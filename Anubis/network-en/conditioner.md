## 用 Network Link Conditioner 来模拟不良网络环境

`Network Link Conditioner` 可以用来精确并持续地模拟不良的网络环境。以最大限度地测试你的 App 在各种网络环境下的运作情况。（**别忘了在完成测试后把它关掉！**）

Network Link Conditioner 可以根据内置的某个预设来改变 iOS 设备的网络环境：

* EDGE
* 3G
* DSL
* WiFi
* High Latency DNS
* Very Bad Network
* 100% Loss


## 在 iOS 设备上启用 Network Link Conditioner

1、在 Xcode 中启用 iOS 设备的开发者模式

* 把你的 iOS 设备连接到 Mac

* 在 Xcode 中，选择 Window > Devices and Simulators（⇧⌘2）

* 在侧边栏中选择你的设备

* 单击 “Use for Development”



2、经过 `1` 的设置后，现在可以在 iOS 设备中进行 `Network Link Conditioner` 配置


a. Setting App > Developer > Network Link Conditioner


![](setting_developer.jpg)


b. 开启 `Network Link Conditioner` 并配置你想要的网络环境

![](conditioner_status.jpg)


c. 或者自定义预设配置来满足你的定制化需求

![](profile.jpg)