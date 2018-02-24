## Sniffer Proxy FAQ

用于局域网中（通常是 WiFi）其它设备的抓包。


### 可以抓哪些设备

所有支持 HTTP 代理设置的设备和应用，如：电脑，其它手机或平板，支持 HTTP 代理的机顶盒或者游戏主机。


### Browser & System HTTP Proxy Configuration

* **macOS HTTP proxy settings**

The macOS proxy settings are configured in the advanced areas of the Network panel in the System Preferences.


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

Export "Thor SSL CA" certificate (.der) of Thor to mac, then install and trust it in Keychain app.


* Windows

* iOS Device

Send a email with "Thor SSL CA" certificate (.der) attatched of Thor to target iOS device's Mail app, then tap attatchment in mail in target device, install and trust it in iOS system.


* Android Device

