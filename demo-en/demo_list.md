## Thor FAQ

<!-- ### -1、申请 TestFlight 免费体验资格

免费体验 7 天 TF 
问卷填写: https://wj.qq.com/s/1607760/e57d -->

### 0. HTTPS decryption

#### Why need a "Thor SSL CA" certificate

HTTPS decryption need the "Thor SSL CA" installed and trusted by iOS system to perform a MiTM for HTTPS traffics.

 A root certificate to perform a MiTM for decoding HTTPS traffics is an unique and standard common view and technology. 


"Thor SSL CA" certificate used in Thor for HTTPS decoding is safe and privacy security, it is generated randomly when Thor first launched and stored in app local keychain only.
Certificates between devices or users are different.

"Thor SSL CA" certificate is unnecessary, if you don't need HTTPS decryption.


#### Trust "Thor SSL CA" in iOS system

You need trust a CA manully after it was installed in `Profiles` since iOS10, as below


`Settings > General > About > Certificate Trust Settings`


#### Why need a VPN tunnel

Thor is a HTTP sniffer, a source of HTTP traffics will be necessary.

Thor used a VPN tunnel to set up a source of HTTP traffics from both WiFi and cellular of local device.

All traffics sniffed by Thor stored in app local only, no records will be uploaded to remote server. (Even Thor doesn't have a remote server or something like it, it is totally a local sniffer tool) 


### 1. Filter in Thor

* **Session Filter**: filter you selected in homepage. It matches keywords or patterns in `Request Headers`.


* **Packet Filter**: filter you selected in packets list. It matches keywords or patterns in `Request Headers`, `Response Headers` and `Response Body` data type.


* Export & Import
	* **f4thor**: file type for `Session Filter` and `Packet Filter`. You can export .f4thor files and share them to anyone or import .f4thor files from someone.

	* **p4thor**: file type for Thor packet records. You can export packets as .p4thor files to backup or share to others who can import and analyze them in Thor.

	* **har**: standard HTTP archive file is supported in Thor.

	* **cURL**: Thor can export requests as curl commands.


