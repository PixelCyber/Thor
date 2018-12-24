# iOS 应用防 HTTPS MiTM 基本方案


## HTTPS MiTM 原理

* [三种解密 HTTPS 流量的方法介绍](https://imququ.com/post/how-to-decrypt-https.html)


## 防 MiTM 原理

* [HTTP Public Key Pinning 介绍](https://imququ.com/post/http-public-key-pinning.html)


## 实现方案 SSL pinning

### 面临的问题

1、SSL 叶子证书问题

域名单一且证书有效期短，大部分为一年。过期后续签时，有可能续签不同的 CA。

2、证书过期问题

* SSL 证书过期后，如果未及时 renew，则影响线上 app 的验证状态。且即使 renew 也会必须发版本更新 app 中的锚点证书。

* 锚点证书推荐使用 Root CA，它的有效期长，二级 CA 数量多，就算 SSL 证书续签换了中级 CA，只要签发祖先是同一个 Root CA，则线上 app 的证书验证不受影响。

* app 内置验证的锚点证书可以根据情况设置多个常见 Root CA，以最大化消除 SSL 证书续签更换证书提供商带来的影响。

**即使遵守以上做法，也不能避免 Root CA 过期的情况，应该在每次 app 更新时，检查更新和补齐锚点证书。**


3、越狱后替换证书绕过验证

越狱设备可以直接替换 app bundle 内的锚点证书为伪造证书，从而绕过验证。

简单的解决办法是：给内置的锚点证书生成摘要，在代码中进行校验，防止证书被篡改。


### 代码实现

1、[Swift 方案参考](https://medium.com/@kennethpoon/lets-write-swift-code-to-intercept-ssl-pinning-https-requests-12446303cc9d)


2、Objective-C + AFNetworking 方案

[a. 内置多个常用 Root CA]()

在 Xcode 中添加物理引用目录，里面放入 Root CA 文件

[b. 利用 Xcode build script 在编译时动态生成证书的带盐摘要文件，并打包到 app 中]()

```bash
PINNED_CA_DIR="${PROJECT_DIR}/你的 Root CA 目录路径"

cd "$PINNED_CA_DIR"

md5 -q *.cer > ca.txt

PINNED_CA_CHECK=`cat ca.txt`
PINNED_CA_CHECK="$PINNED_CA_CHECK"+"${PINNED_CA_SALT}"

md5 -q -s "$PINNED_CA_CHECK" > ca.check

```

以上脚本会在编译时向 Root CA 所在目录生成两个文件：

* `ca.txt`: 证书摘要列表

* `ca.check`: 证书摘要列表的带盐摘要
  

脚本中引用的变量：

* `PINNED_CA_SALT`: 盐，配置在 Xcode User-Defined 中，且 `PINNED_CA_CHECK` 可以根据需要自由组合


[c. 代码校验摘要及证书验证]()

定义 AFSecurityPolicy (属于 AFNetworking) 的子类 XXSecurityPolicy

```objective-c
@implementation XXSecurityPolicy

+ (instancetype)defaultPolicy
{    
    static XXSecurityPolicy *securityPolicy = nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        @autoreleasepool {
            NSMutableSet<NSData *> *set = NSMutableSet.set;
            NSURL *dir = [NSBundle.mainBundle.resourceURL URLByAppendingPathComponent:@"Root CA 所在目录" isDirectory:YES];
            
            BOOL valid = NO;
            do {
                NSURL *checkFile = [dir URLByAppendingPathComponent:@"ca.check"];
                NSString *checksum = [NSString stringWithContentsOfURL:checkFile encoding:NSUTF8StringEncoding error:NULL];
                checksum = [checksum stringByTrimmingCharactersInSet:NSCharacterSet.whitespaceAndNewlineCharacterSet];
                if (checksum.length != 32U) {
                    NSAssert(false, @"pinned ca files check checksum failed.");
                    break;
                }
                
                NSURL *checListFile = [dir URLByAppendingPathComponent:@"ca.txt"];
                NSString *checkListStr = [NSString stringWithContentsOfURL:checListFile encoding:NSUTF8StringEncoding error:NULL];
                checkListStr = [checkListStr stringByTrimmingCharactersInSet:NSCharacterSet.whitespaceAndNewlineCharacterSet];
                
                NSString *const salt = @(PINNED_CA_SALT);
                NSMutableString *md5Str = NSMutableString.string;
                [md5Str appendString:checkListStr];
                [md5Str appendString:@"+"];
                [md5Str appendString:salt];
                NSString *md5 = md5Str.MD5_32;
                if (![md5 isEqualToString:checksum]) {
                    NSAssert(false, @"pinned ca files check checksum failed.");
                    break;
                }
                
                NSArray<NSString *> *checkList = [checkListStr componentsSeparatedByString:@"\n"];
                if (checkList.count < 1) {
                    break;
                }
                
                for (NSString *file in [NSFileManager.defaultManager contentsOfDirectoryAtPath:dir.path error:NULL]) {
                    @autoreleasepool {
                        if (![file.pathExtension isEqualToString:@"cer"]) {
                            continue;
                        }
                        NSData *data = [NSData dataWithContentsOfURL:[dir URLByAppendingPathComponent:file] options:NSDataReadingUncached|NSDataReadingMappedAlways error:NULL];
                        if (nil != data && [checkList containsObject:data.MD5String ?: @""]) {
                            [set addObject:data];
                        }
                    }
                }
                
                NSAssert(set.count == checkList.count, @"pinned ca files check checksum failed.");
                if (set.count == checkList.count) {
                    valid = YES;
                }
            } while (false);
            
            if (!valid) {
                exit(0);
            }
#ifdef DEBUG
            securityPolicy = [super defaultPolicy];
#else
            securityPolicy = [self policyWithPinningMode:AFSSLPinningModeCertificate withPinnedCertificates:set];
#endif
        }
    });
    
    return securityPolicy;
}

- (BOOL)evaluateServerTrust:(SecTrustRef)serverTrust
                  forDomain:(NSString *)domain
{
    if ([super evaluateServerTrust:serverTrust forDomain:domain]) {
        return YES;
    }
    
    switch (self.SSLPinningMode) {
        case AFSSLPinningModeNone:
        default:
            return NO;
            
        case AFSSLPinningModeCertificate: {
            if (self.pinnedCertificates.count < 1) {
                return NO;
            }
            
            CFIndex certificateCount = SecTrustGetCertificateCount(serverTrust);
            if (certificateCount < 1) {
                return NO;
            }
            
            SecCertificateRef certificate = SecTrustGetCertificateAtIndex(serverTrust, certificateCount - 1);
            if (NULL == certificate) {
                return NO;
            }
            
            NSData *rootCA = (__bridge_transfer NSData *)SecCertificateCopyData(certificate);
            if (![self.pinnedCertificates containsObject:rootCA]) {
                return NO;
            }
            
            NSMutableArray *policies = NSMutableArray.array;
            if (self.validatesDomainName) {
                [policies addObject:(__bridge_transfer id)SecPolicyCreateSSL(true, (__bridge CFStringRef)domain)];
            } else {
                [policies addObject:(__bridge_transfer id)SecPolicyCreateBasicX509()];
            }
            
            SecTrustSetPolicies(serverTrust, (__bridge CFArrayRef)policies);
            NSMutableArray *pinnedCertificates = NSMutableArray.array;
            for (NSData *certificateData in self.pinnedCertificates) {
                [pinnedCertificates addObject:(__bridge_transfer id)SecCertificateCreateWithData(NULL, (__bridge CFDataRef)certificateData)];
            }
            SecTrustSetAnchorCertificates(serverTrust, (__bridge CFArrayRef)pinnedCertificates);
            
            SecTrustResultType result = kSecTrustResultInvalid;
            OSStatus os = SecTrustEvaluate(serverTrust, &result);
            if (result == kSecTrustResultUnspecified || result == kSecTrustResultProceed) {
                return YES;
            }
            
            if (errSecCertificateExpired == os || result == kSecTrustResultRecoverableTrustFailure) {
                return YES;
            }
            
            return NO;
        }
    }
}

```

代码中用的宏 `PINNED_CA_SALT` 在 Xcode > Build Settings > Preprocessor Macros 定义为

```bash
# 后面的 PINNED_CA_SALT 是之前定义的 User-Defined 常量
PINNED_CA_SALT=\"$(PINNED_CA_SALT)\"
```

*默认实现中，如果摘要校验不通过，会直接 exit 进程，可根据实际需要自行决定处理方式。*

*默认实现中，如果锚点证书合法但是过期，则继续信任并通过，可根据实际需要自行决定处理方式。*
