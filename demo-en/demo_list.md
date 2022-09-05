## Thor FAQ


### 0. HTTPS decryption

#### Why need a "Thor SSL CA" certificate

HTTPS decryption need the "Thor SSL CA" installed and trusted by system to perform a MiTM for HTTPS traffics.

 A root certificate to perform a MiTM for decoding HTTPS traffics is an unique and standard common view and technology. 


"Thor SSL CA" certificate used in Thor for HTTPS decoding is safe and privacy security, it is generated randomly when Thor first launched and stored in app local keychain only.
Certificates between devices or users are different.

"Thor SSL CA" certificate is unnecessary, if you don't need HTTPS decryption.


#### Trust "Thor SSL CA" in iOS system

You need trust a CA manually after it was installed in `Profiles` since iOS10, as below


`Settings > General > About > Certificate Trust Settings`


#### Why need a VPN tunnel

Thor is a HTTP sniffer, a source of HTTP traffics will be necessary.

Thor used a VPN tunnel to set up a source of HTTP traffics from both Wi-Fi and cellular of local device.

All traffics sniffed by Thor stored in app local only, no records will be uploaded to remote server. (Even Thor doesn't have a remote server or something like that, it's totally a local sniffer tool.) 

