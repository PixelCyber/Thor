## Thor FQA

<!-- ### -1、申请 TestFlight 免费体验资格

免费体验 7 天 TF 
问卷填写: https://wj.qq.com/s/1607760/e57d -->

### 0. HTTPS decryption

#### Why need a "Thor SSL CA" certificate

HTTPS decryption need the "Thor SSL CA" installed and trusted by iOS system to perform a MiTM for HTTPS traffics.

"Thor SSL CA" is unnecessary, if you don't need HTTPS decryption.


#### Trust "Thor SSL CA" in iOS system

You need trust a CA manully since iOS11 after it was installed in `Profiles`, as below


`Settings > General > About > Certificate Trust Settings`