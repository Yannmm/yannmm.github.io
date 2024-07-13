---
layout: post
title: "Futter Automation Testing: Appium"
tags: flutter test
---

![Appium Architecture](https://i.postimg.cc/1zR3Mc1f/appium-architecture.jpg)

`Appium` is an open-source mobile app testing framework.

`Appium Server` is a web server running either locally or remotely, which handles communications between `Appium Client` and Application Under Test (AUT). For the former purpose, it serves `JSON wire protocol`; for the latter one, it implements `WebDriver protocol`.

`Appium Client` converts commands into HTTP requests, sending to the server. A variety of client language bindings are provided, meaning test cases in Appium can be written in Java, Python, JavaScript, and PHP etc.

`Robot Framework` acts as a Python wrapper of `Appium Client`. It features human-friendly DSL syntax using keywords. It converts DSLs into Appium commands, passing to the underlying client.


To interact with target device, Appium works in differernt ways on iOS and Android. 
    - On iOS, an IPA of `WebDriverAgent.app` is installed on the target device and it acts as a running server. It listens to commands in WebDriver format and translates into `XCUITest` code. It employs `XCUITest Framework` to control AUT and simulates user intractions. After execution, return response to `Appium Server`.
    - On Android, the workflow is exactly the same, only to replace WebDriverAgent.app IPA with `Bootstrap.jar` APK and XCUITest Framework with `UI Automator Framework`.

To facilitate above process, `Appium Server` also needs to intall drivers: `XCUITest driver` for IOS, `UIAutomator2 driver` for Android and `Appium Flutter driver` for Flutter. The last one utilizes the first two underneath.

`Appium Flutter driver` also dependeds on `flutter_driver` in pubspec.yaml of AUT Flutter project.

**References**

- [Appium Architecture, Explained](https://www.waldo.com/blog/appium-architecture)
- [Appium](https://github.com/appium/appium)
- [Appium Server](https://appium.io/docs/en/2.6/intro/appium/)
- [Appium Cient](https://appium.io/docs/en/2.6/intro/clients/)
- [JSON wire protocol]()
- [WebDriver protocol]()
- [Robot Framework](https://robotframework.org/)
- [XCUITest Framework](https://www.browserstack.com/guide/getting-started-xcuitest-framework)
- [XCUITest driver](https://github.com/appium/appium-xcuitest-driver)
= [WebDriverAgent.app](https://appium.github.io/appium-xcuitest-driver/4.24/wda-custom-server/)
- [UI Automator Framework](https://developer.android.com/training/testing/other-components/ui-automator)
- [UiAutomator2 driver](https://github.com/appium/appium-uiautomator2-driver)
- [Appium Flutter driver](https://github.com/appium/appium-flutter-driver)
- [flutter_driver](https://api.flutter.dev/flutter/flutter_driver/flutter_driver-library.html)


