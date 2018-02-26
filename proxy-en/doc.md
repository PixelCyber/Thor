## Sniffer Proxy FAQ

Sniff other devices in the same LAN with Thor.


### What can be sniffed by Thor

Devices or applications support HTTP Proxy, such as Mac/PC, iOS device, Android device, PS4/Xbox etc.


### Browser & System HTTP Proxy Configuration

* **macOS HTTP proxy settings**

System Preferences > Network > Choose a network to configure > Advanced > Proxy.


* **Windows / Internet Explorer HTTP proxy settings**

The Windows proxy settings are configured in the Internet Options control panel on the Connections tab.
Microsoft Edge has an additional setting that you may need to make by browsing to about:flags.


* **Mozilla Firefox HTTP proxy settings**

Configure Firefox to use your system proxy settings. In Firefox, go to Preferences > Advanced > Network > Connection Mozilla Firefox can now be configured to use the system proxy settings.

Check your Firefox proxy settings in Preferences > Advanced > Network > Connection and press the Settings button. Then choose "Use system proxy settings".


* **iOS Device HTTP proxy Settings**

Go to the Settings app, tap Wi-Fi, find the network you are connected to and then tap it to configure the network. Scroll down to the HTTP Proxy setting, tap Manual. Enter the IP address of your Thor in the Server field, and the port on in the Port field (usually 8423). Leave Authentication set to Off.

Remember to disable the HTTP Proxy in your Settings when you stop using Thor, otherwise you'll get confusing network failures in your applications!


* **Android Device HTTP proxy Settings**

Some Android devices have HTTP proxy settings. On the Nexus S it is hidden; you can access the HTTP proxy settings by opening the Voice Dialler app and saying "proxy". On some Samsung devices you can access proxy settings by long-pressing on the network name in the WiFi configuration.


### Trust Thor SSL CA on your device

* macOS

Export "Thor SSL CA" certificate (.der) to mac, then install and trust it in Keychain app.

Double click "Thor SSL CA" on macOS > Find it in Keychain > Get Info > Always Trust.


* Windows

Export "Thor SSL CA" certificate (.der) to Windows, then install and trust it in ` Trusted Root Certification Authorities store`.


* iOS Device

	* Send a email with "Thor SSL CA" certificate (.der) attatched of Thor to target iOS device's Mail app, then tap attatchment in mail in target device, install and trust it in iOS system.

	* Export "Thor SSL CA" certificate (.der) to target device and save it to File app > iCloud Driver, then install it in iCloud Driver of File app.


<!-- * Android Device -->

* Mozilla Firefox

Preferences > Options > Privacy & Security > Certificates > View Certificates > Certificate Authority > click Import button in bottom and import your "Thor SSL CA" > Check all the trust options > Confirm

