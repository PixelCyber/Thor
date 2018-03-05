## Thor HTTP 抓包分析 for iOS

![](thor_logo.jpg)

iOS 端强力专业的 HTTPS 抓包分析工具 - Thor

[去 App store 下载](https://itunes.apple.com/app/id1210562295)

另一个作品 Shu，跟 Thor 搭配使用，获得最佳体验, [买 Thor 送 Shu 同捆包](https://itunes.apple.com/app-bundle/id1333938041)


[Product Hunt 应用主页](https://www.producthunt.com/posts/thor)

其它语言: [English](README.md).


欢迎大家交流讨论抓包技巧：[官推](https://twitter.com/thor_pixelcyber)、[tg 群](https://t.me/thorshu)、[tg 频道](https://t.me/thornotice)


### 特点

- 免配 https 域名，自动高性能解析所有 HTTPS 流量

- 支持 WiFi 局域网代理（抓取其他设备的 HTTP 流量）
```
无需电脑随时抓包，购买一次随处使用，过滤器配置轻松复用
```
[wifi 代理设置](res/wifi_proxy.jpg)

![](res/thumbnail/wifi_proxy.jpg)

- 独创的过滤器筛选技术（f4thor），让你一键得到目标数据
```
得益于 Thor 灵活全面的过滤器和筛选器配置规则，数据过滤和数据分析从未如此简单
导出自己的过滤器配置，抓包数据，共享工作成果，即使是小白也能从中受益
```
[过滤器管理及导出导入](res/sessin_filter_export.jpg)

![](res/thumbnail/sessin_filter_export.jpg)


[过滤器配置](res/session_filter.jpg)

![](res/thumbnail/session_filter.jpg)


[筛选器配置](res/packet_filter.jpg)

![](res/thumbnail/packet_filter.jpg)


[筛选器-记录搜索](res/search.jpg)

![](res/thumbnail/search.jpg)



- 最全面的 HTTP body 解析，预览及分析支持
```
支持几乎所有常见文件类型的解析和预览
```

- 全面专业的数据格式导出支持
```
行业标准的 har, cURL 格式批量导出

Thor 独创的 p4thor 记录格式让包记录协作分析和共享备份变得简单快捷
```
[抓包记录导出](res/packet_export.jpg)

![](res/thumbnail/packet_export.jpg)

- 超强的性能和高稳定性让 iOS9 也能发挥极致
```
超长时间稳定运行，成千上万的数据实时记录并刷新
```


### 现有计划

Thor 从去年 3月20日上架起，经过一年的迭代，功能，性能，稳定性已日渐成熟，是时候向大家推荐 Thor 了。

Thor 的版本已经规划到 1.7 （现在是 1.3），接下来的版本会陆续完成`断点调试`，`请求重放`，`过滤器前置后置操作`等更加强大的功能。



![](https://is1-ssl.mzstatic.com/image/thumb/Purple111/v4/61/0f/87/610f87ff-4c81-fcc3-4b38-58bce34eed9b/source/230x0w.jpg)
![](https://is5-ssl.mzstatic.com/image/thumb/Purple118/v4/0c/f7/b1/0cf7b1f4-9a19-271b-2172-8e3ec941c9af/source/230x0w.jpg)
![](https://is5-ssl.mzstatic.com/image/thumb/Purple128/v4/4b/f9/8f/4bf98ffb-1ab4-6d0b-2a04-1da90cdf6cd6/source/230x0w.jpg)
![](https://is1-ssl.mzstatic.com/image/thumb/Purple118/v4/b0/f2/44/b0f2446a-ca64-7d38-ec88-90b339b431f6/source/230x0w.jpg)
![](https://is3-ssl.mzstatic.com/image/thumb/Purple128/v4/19/a1/d0/19a1d063-2c53-1283-d123-1814e2ef082a/source/230x0w.jpg)


### 免费参加 TestFlight 体验 Thor

- 填写问卷：[https://wj.qq.com/s/1607760/e57d](https://wj.qq.com/s/1607760/e57d)

[**使用技巧 >>**](tips-zh-Hans/dev_tip.md)

[**常见问题 >>**](demo-zh-Hans/demo_list.md)


### 功能

Thor 无法与其它『微屁恩』同时打开，不支持任何科学上网功能。

灵活强大的过滤，筛选规则配置：

- 支持按域名，关键字等配置过滤
- 抓到的结果支持各种条件的筛选
- 关键字搜索
- 过滤规则 f4thor 导入导出（轻松使用别人分享的过滤器配置）
- 抓取局域网（WiFi）内其它设备的 HTTP 流量

三方 App 文件查看及解压：

- 常见文件查看
- 证书预览及格式转换导出及安装到系统（der, pem, p12）
- 解压(含密码)：zip, rar, 7z, tgz, tar, bz, tbz, gz, lz4
- 字体文件预览

自动解析包数据：

- 自动解析 HTTP 消息体为常见媒体形式
- 支持导出原始请求数据
- 包记录添加备注

强悍优异的性能：

- 边抓边看，请求的生命周期状态实时更新
- 轻松实时记录成千上万个 HTTP 请求
- 保持整天打开也不会对网络日常使用造成影响
- iOS9 上也能持续稳定工作

HTTP(S) 抓包：

- HTTPS 高性能实时解析
- HTTP pipelining
- websocket 流量抓取
- cURL, .har, .f4thor, p4thor 导入导出
- 通知中心的 HTTP 抓包 widget 可实时查看最新抓到的包
- 抓包过程中支持一键清空当前记录
- iPad 分屏抓包
- 请求包支持文本备注和收藏


**不支持抓取 TCP，UDP 流量**