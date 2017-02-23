# Applesss ![GPLv3 License](https://img.shields.io/badge/License-GPLv3-blue.svg)

 

Applesss is an iOS client that implements custom proxies with the leverage of Network Extension framework introduced by Apple since iOS 9.

Currently, Applesss is compatible with following proxies:

- [Shadowsocks](https://shadowsocks.org)
- [ShadowsocksR](https://github.com/breakwa11/shadowsocks-rss)


## Project Info

Applesss has in total 31 dependencies as following

* 28 Cocoapod dependencies
* 1 Carthage dependency
* 2 submodules dependencies

The project is tested with Xcode 8.2 (8C38) on iOS 10.2 (14C92) device with cocoapod version `1.1.1`.

## Set up Guide - Code

Perform the following steps to be able to build the project.
Be warned that you **should not** call `pod update` as newer version of pod frameworks that Applesss depends on might break building process and there will be errors.

1. `git submodule update --init` to update git submodule
2. `pod install` to pull down dependencies into our project
3. `carthage update` to pull down dependencies into `Carthage/Checkouts` folder and build each one
4. Open Xcode **workspace** project (`Applesss.xcworkspace`).
   1. Click on Applesss project, then click on `General` tap.
   2. Click on `Applesss` target at Targets section.
   3. Change its `Bundle Identifier` to match with your desire domain name for example `com.yourdomain.Applesss`.
   4. For the following targets, you change `io.wasin.Applesss` to match your domain name. This means if you see `io.wasin.Applesss.tunnel`, you change it to `com.yourdomain.Applesss.tunnel`.
      * `PacketTunnel`
      * `TodayWidget`
      * `ApplesssLibrary`
      * `PacketProcessor`
      * `ApplesssModel`
      * `ApplesssBase`
5. Follow the guide in *Set up Guide - Apple Developer Website* section.
6. Build and Run the project. Done.

## Set up Guide - Apple Developer Website

Note that it's better to not allow Xcode to automatically manage your provisioning profile for the application included Applesss (main app), PacketTunnel (extension), and TodayWidget (extension). Most of the time, such provisioning profile won't generate on developer page, or point to generic one which makes it not working!.

So follow the following steps

* Create 3 App IDs for `Applesss`, `PacketTunnel`, and `TodayWidget` on Apple Developer website. Make sure to name bundle id for each one matches bundle identifier you used when setting up with Xcode. In this case `io.wasin.Applesss`, `io.wasin.Applesss.tunnel`, and `io.wasin.Applesss.todaywidget` respectively. Rename to be your domain name freely.
   * **`Applesss`**  
      Enable `App Groups`, `Game Center`, `iCloud`, `In-App Purchase`, `Network Extensions`, and `Push Notifications`.
   * **`PacketTunnel`**  
      Enable `App Groups`, `Game Center`, `In-App Purchase`, and `Network Extensions`.
   * **`TodayWidget`**  
      Enable `App Groups`, `Game Center`, `In-App Purchase`, and `Network Extensions`.

* Create 3 corresponding provisioning profile for each created App ID on Apple Developer website.
* Now go back to Xcode
* Click on project -> click on General tap -> select `Applesss` target and uncheck "Automatically manage signing" -> select a proper provisioning profile in both "Signing (Debug)" and "Signing (Release)".
* Do the same for `PacketTunnel` and `TodayWidget` target.

## Code Notices

There're a couple of issues that needed to look at, but at tested, it doen **not** effect the functionality of the app.

* In file `Applesss/Core/API.swift`, it's the following code focusing on line with comment that I can't figure it out yet how to migrate it to Swift 3 code.  

   ```swift
   var JSONToMap: AnyObject?
   if let keyPath = keyPath, keyPath.isEmpty == false {
       //JSONToMap = (result.value? as AnyObject).value(forKeyPath: keyPath)
       JSONToMap = nil
   } else {
       JSONToMap = result.value as AnyObject?
   }
   ```
* Applesss core code depends on version `1.7.0` of Eureka with manual migration to Swift 3. It's already done and linked to project. But you will see `observeValue()` function in `Eureka/Source/Rows/PostalAddressRow.swift` that has been commented for all of its function code due to Eureka's newer version `2.0.0-beta.1` doesn't include such file in the project anymore, but it still works with no problem. This note is meant to mark that there is going to be a lot of effort if we decide to depend on Eureka version `2.0.0-beta.1` as we need to change a lot of Applesss core code.

## How To Contribute

Clone the project, make some changes or add a new feature, then make a pull request.

## Support Us

The development covers a lot of complicated work, costing not only money but also time.



## Acknowlegements

We use the following services or open-source libraries. So we'd like show them highest respect and thank for bringing those great projects:

Services:

- [Fabric](https://get.fabric.io/)
- [Reveal](http://revealapp.com/)
- [realm](https://realm.io/)
- [HelpShift](https://www.helpshift.com)

Open-source Libraries:

- [KissXML](https://github.com/robbiehanson/KissXML)
- [MMWormhole](https://github.com/mutualmobile/MMWormhole)
- [CocoaAsyncSocket](https://github.com/robbiehanson/CocoaAsyncSocket)
- [Cartography](https://github.com/robb/Cartography)
- [AsyncSwift](https://github.com/duemunk/Async)
- [Appirater](https://github.com/arashpayan/appirater)
- [Eureka](https://github.com/xmartlabs/Eureka)
- [MBProgressHUD](https://github.com/matej/MBProgressHUD)
- [CallbackURLKit](https://github.com/phimage/CallbackURLKit)
- [ISO8601DateFormatter](https://github.com/boredzo/iso-8601-date-formatter)
- [Alamofire](https://github.com/Alamofire/Alamofire)
- [ObjectMapper](https://github.com/Hearst-DD/ObjectMapper)
- [CocoaLumberjack](https://github.com/CocoaLumberjack/CocoaLumberjack)
- [AlamofireObjectMapper](https://github.com/tristanhimmelman/AlamofireObjectMapper)
- [YAML.framework](https://github.com/mirek/YAML.framework)
- [tun2socks-iOS](https://github.com/shadowsocks/tun2socks-iOS)
- [shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev)
- [Antinat](http://antinat.sourceforge.net/)
- [Privoxy](https://www.privoxy.org/)
