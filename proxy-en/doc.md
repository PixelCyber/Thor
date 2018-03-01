## Sniffer Proxy FAQ

Sniff and debug HTTP traffic on other devices in same LAN with Thor.


### What can be sniffed with Thor

Devices or applications support HTTP Proxy, such as Mac/PC, iOS device, Android device, PS/Xbox, etc.


### 1. Browser & System HTTP Proxy Configuration

#### macOS HTTP proxy settings

a. Go to `System Preferences > Network > Choose a network to configure > Advanced > Proxies`

b. Check `Web Proxy (HTTP)` and `Secure Web Proxy (HTTPS)`

c. Enter proxy server address and port of Thor


#### Windows / Internet Explorer HTTP proxy settings

Network > Connections > Internet Options control panel

Microsoft Edge has an additional setting that you may need to make by browsing to `about:flags`.


#### Mozilla Firefox HTTP proxy settings

Configure Firefox to use your system proxy settings. 

In Firefox, go to Preferences > General > HTTP Proxy > Mozilla Firefox can now be configured to use the system proxy settings.


#### iOS Device HTTP proxy Settings

Go to `Settings app > Wi-Fi > find the network you are connected to and then tap it to configure the network > Scroll down to the HTTP Proxy setting > tap Manual > Enter the proxy address and port of Thor`

Remember to disable the HTTP Proxy in your Settings when you stop using Thor, otherwise you'll get confusing network failures in your applications!


#### Android Device HTTP proxy Settings

Some Android devices have HTTP proxy settings. On the Nexus S it is hidden; you can access the HTTP proxy settings by opening the Voice Dialler app and saying "proxy". On some Samsung devices you can access proxy settings by long-pressing on the network name in the WiFi configuration.


### 2. Trust Thor SSL CA on your device

"Thor SSL CA" certificate used in Thor for HTTPS decoding is safe and privacy security, it is generated randomly when Thor first launched and stored in app local keychain only.
Certificates between devices or users are different.

"Thor SSL CA" certificate is unnecessary, if you don't need HTTPS decryption.


#### macOS

Export "Thor SSL CA" certificate (.der) to mac, then install and trust it in Keychain app.

Double click "Thor SSL CA" on macOS > Find it in Keychain > Get Info > Always Trust.


#### Windows

Export "Thor SSL CA" certificate (.der) to Windows, then install and trust it in ` Trusted Root Certification Authorities store`.


#### iOS Device

* Send a email with "Thor SSL CA" certificate (.der) attatched of Thor to target iOS device's Mail app, then tap attatchment in mail in target device, install and trust it in iOS system.

* Export "Thor SSL CA" certificate (.der) to target device and save it to File app > iCloud Driver, then install it in iCloud Driver of File app.


<!-- #### Android Device -->


#### Mozilla Firefox

Mozilla Firefox has its own Certificate Authority, Certificate Authority of system would not work on it.

Preferences > Security & Privacy > View Certificates > Certificate Authority > click Import button in bottom and import your "Thor SSL CA" > Check all the trust options > Confirm

