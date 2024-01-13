# Android 版本适配全套指南

* 项目地址：[Github](https://github.com/getActivity/AndroidVersionAdapter)

* 当我在做 Android 版本适配工作的时候很痛苦，那个时候我在想有没有一个文档，将所有的关于 Android 版本适配资料全部收集起来，这样就不需要在网上东找西找了，这样就能把时间和精力投入适配工作中，每当一个新的 Android 版本发布的时候，这个想法越加强烈，终于在 Android 11 刚发布的时候筹划了这件事情，最终赶在 Android 12 刚发布的时候完成了，整个过程耗时非常漫长，因为我正在不断收集优质的资料，同时我也在不断思考，什么样的适配文档才是大家所需要的，我将适配文档简单划分成了以下几部分：

    * 官方文档

        * 新特性

        * 行为变更

    * 相关资源

        * 适配文章链接

        * 适配框架链接

* 为什么要把这个做成开源项目？因为我会不断更新，同时欢迎大家如果有好的文章也可以通过 [issue](https://github.com/getActivity/AndroidVersionAdapter/issues/new) 推荐给我，我审核通过之后会放上去，做好一个开源项目需要大家的添砖加瓦，开源是一个互帮互助的过程，没有大家的支持我很难做好它。

## 适配流程

* 这里以适配 `Android 14` 为例子，第一步将主模块中的 `build.gradle` 文件中修改 `targetSdkVersion` 和 `compileSdkVersion` 这两个的值

```groovy
android {

    compileSdkVersion 34
    defaultConfig {
        ......
        targetSdkVersion 34
    }
}
```

* 接下来在代码中做一些版本的判断，并且做好新版本的适配和旧版本的兼容

```java
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.UPSIDE_DOWN_CAKE) {
    ......
} else {
    ......
}
```

```java
if (context.getApplicationInfo().targetSdkVersion >= Build.VERSION_CODES.UPSIDE_DOWN_CAKE) {
    ......
} else {
    ......
}
```

* 到这里，大家可能有一个疑问，targetSdkVersion 和 compileSdkVersion 有啥区别？

    * targetSdkVersion：目标适配版本，告知系统 App 适配的情况，如果应用的 targetSdkVersion 比系统版本要低，那么在一些新特性上新系统会做向下兼容性处理，如果我们想要适配某个 Android 版本，必须要将 targetSdkVersion 调整到这个版本等级之上，否则在某些机型上面可能会出现一些适配异常的情况。如果我们只是简单调高了 targetSdkVersion 等级而没有适配新版本的特性，那么应用在新系统上可能会出现功能异常的情况，一般情况表现为应用崩溃或者获取不到数据。

    * compileSdkVersion：编译源码版本，我们可以通过修改这个版本等级来改变我们在代码中所看到的 Android SDK 源码的版本，同时也决定了编译器在进行代码检查时所用的版本。

* 最后附上一张 Android 版本信息对应表

| Android 版本 | API 等级 |      版本代号       | 市场占有率  |        发布时间       |
| :--------:  | :-----: |:------------------:|:---------:| :------------------: |
| Android 14  |    34   | `UPSIDE_DOWN_CAKE` |  暂无数据  |  2023 年 10 月 10 日   |
| Android 13  |    33   |     `TIRAMISU`     |  30.33%  |  2022 年 8 月 16 日   |
| Android 12L |    32   |       `S_V2`       |  暂无数据 |  2022 年 3 月 9 日    |
| Android 12  |    31   |        `S`         |  20.58% |  2021 年 10 月 4 日   |
| Android 11  |    30   |        `R`         |  19.98% |  2020 年 9 月 9 日    |
| Android 10  |    29   |        `Q`         |  9.27%  |  2019 年 9 月 3 日    |
| Android 9.0 |    28   |        `P`         |  8.61%  |  2018 年 8 月 7 日    |
| Android 8.1 |    27   |      `O_MR1`       |  2.78%  |  2017 年 12 月 5 日   |
| Android 8.0 |    26   |        `O`         |  3.21%  |  2017 年 8 月 22 日   |
| Android 7.1 |    25   |      `N_MR1`       |  0.61%  |  2016 年 12 月 5 日   |
| Android 7.0 |    24   |        `N`         |  1.88%  |  2016 年 8 月 22 日   |
| Android 6.0 |    23   |        `M`         |  1.64%  |  2015 年 9 月 29 日   |
| Android 5.1 |    22   |   `LOLLIPOP_MR1`   |  0.98%  |  2015 年 3 月 10 日   |
| Android 5.0 |    21   |     `LOLLIPOP`     |  0.53%  |  2014 年 10 月 15 日  |
| Android 4.4 |    19   |      `KITKAT`      |   0.3%  |  2013 年 10 月 31 日  |

* 市场占用率数据更新至 2023 年 11 月 5 日，数据统计主要参考以下链接：

* [Android API Levels](https://apilevels.com/)

* [分发信息中心（谷歌官方）](https://developer.android.google.cn/about/dashboards?hl=zh-cn)

* [Top Android OS versions（需要翻墙）](https://www.appbrain.com/stats/top-android-sdk-versions)

* [Mobile & Tablet Android Version Market Share Worldwide](https://gs.statcounter.com/android-version-market-share/mobile-tablet/worldwide)

* [Mobile Android operating system market share by version worldwide from January 2018 to January 2022](https://www.statista.com/statistics/921152/mobile-android-version-share-worldwide/)

## Google Play 应用商店政策

* [Google Play 应用在目标 API 级别方面需满足的要求（需要翻墙）](https://support.google.com/googleplay/android-developer/answer/11926878?hl=zh-Hans)

* 每个新的 Android 版本都会引入一些变化，以便改进安全性和性能，并提升 Android 的整体用户体验。每款应用的清单文件中都有一个 `targetSdkVersion` 参数（也称为目标 API 级别），用以告知系统您的应用在不同的 Android 版本上分别该如何运行。

* 将应用的目标 API 级别配置为新近的 API 级别可确保用户享受到安全性、隐私保护和性能方面的改进，同时仍然允许应用在较低版本的 Android（低至 `minSdkVersion`）上运行。

* 为了向 Android 和 Google Play 用户提供安全可靠的使用体验，Google Play 要求所有应用在目标 API 级别方面都必须符合下列要求。

#### 名词定义

|  新应用  | 尚未在 Play 商店中发布的应用（例如，全新的应用） |
| :-----: | :---------------------------------------: |
| 应用更新 |       已在 Play 商店中发布的应用的新版本      |
| 现有应用 |           没有获得更新的已发布应用           |

#### 何时必须将 Google Play 应用的目标 API 级别设为该级别？

|    Android 操作系统版本   |       新应用      |       应用更新     |       现有应用         |    
| :---------------------: | :--------------: | :--------------: | :----------------: |
| Android 13（API 级别 33）| 2023 年 8 月 1 日 | 2023 年 11 月 1 日 | 2024 年 11 月 1 日 |
| Android 12（API 级别 31）| 2022 年 8 月 1 日 | 2022 年 11 月 1 日 | 2023 年 11 月 1 日 |
| Android 11（API 级别 30）| 2021 年 8 月 1 日 | 2021 年 11 月 1 日 | 2022 年 11 月 1 日 |

**提示**：如需获得技术指导来了解如何更改应用的目标 API 级别以满足上述要求，请参阅[迁移指南](https://developer.android.google.cn/distribute/best-practices/develop/target-sdk.html)。

#### 何时必须将 Wear OS 应用的目标 API 级别设为该级别？

|    Android 操作系统版本   |       新应用      |       应用更新     |       现有应用      |    
| :---------------------: | :--------------: | :--------------: | :----------------: |
| Android 11（API 级别 30） | 2022 年 8 月 1 日 | 2022 年 11 月 1 日 |       无要求      |
| Android 10（API 级别 29） |       无要求      |       无要求       |       无要求      |
| Android 9（API 级别 28）  | 2019 年 8 月 1 日 | 2019 年 11 月 1 日 |       无要求      |

* 为帮助开发者轻松完成过渡，相比新应用，我们多给了应用更新几个月时间来满足该要求。

#### 应用可能受到的影响

* 您的应用若不符合目标 API 级别要求，可能会受到以下方面的影响：

| **应用** |                            **影响**                           |
| -------- | ------------------------------------------------------------ |
| 新应用   | 您将无法在 Play 管理中心发布不符合目标 API 级别要求的 app bundle。 |
| 应用更新 | 您将无法在 Play 管理中心提交不符合目标 API 级别要求的 app bundle 或 APK。 |
| 现有应用 | 如果新用户的设备搭载的 Android 操作系统版本高于您的应用的目标 API 级别，那么这类用户将无法在 Google Play 上获取您的应用。也就是说，这类新用户将无法从 Google Play 中发现或安装您的应用。之前从 Google Play 中安装过这款应用的用户仍可以发现、重新安装和使用它。这类现有用户即使换用新的 Android 设备，也仍然可以使用您的应用。 |

* 为帮助开发者轻松完成过渡，相比新应用，我们多给了应用更新几个月时间来满足该要求。

## 文档目录

* [Android 14.0](#android-140)

* [Android 13.0](#android-130)

* [Android 12.0 / 12L](#android-120--12l)

* [Android 11.0](#android-110)

* [Android 10.0](#android-100)

* [Android 9.0](#android-90)

* [Android 8.0 / 8.1](#android-80--81)

* [Android 7.0 / 7.1.1](#android-70--711)

* [Android 6.0](#android-60)

* [Android 5.0 / 5.1](#android-50--51)

* [Android 4.4](#android-44)

## Android 14.0

#### 新特性

* [国际化](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#i18n)

    * [各应用语言偏好设定](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#app-languages)

    * [语法变化 API](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#app-languages)

    * [地区偏好设置](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#regional-preferences)

* [无障碍](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#accessibility)

    * [非线性字体放大至 200%](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#non-linear-font-scaling)

* [用户体验](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#ux)

    * [Sharesheet 自定义操作和经过改进的排名系统](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#sharesheet-improvements)

    * [支持内置和自定义预测性返回动画](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#predictive-back-animations)

    * [针对应用商店的改进](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#app-stores)

    * [检测用户何时截取设备屏幕截图](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#screenshot-detection)

* [图形](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#graphics)

    * [路径现在可查询和插值](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#paths)

* [核心功能](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#core)

    * [OpenJDK 17 更新](https://developer.android.google.cn/about/versions/14/features?hl=zh-cn#core-libraries)

#### 行为更变

* [针对所有应用的行为变更](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn)

    * [核心功能](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#core)

        * [默认拒绝设定精确的闹钟](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#schedule-exact-alarms)

        * [当应用进入缓存时，上下文注册的广播将加入队列](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#pending-broadcasts-queued)

        * [应用只能终止自己的后台进程](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#kill-own-background-processes)

    * [安全](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#security)

        * [最低可安装的目标 API 级别](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#minimum-target-api-level)

        * [媒体所有者软件包名称可能会隐去](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#media-owner-package-names)

    * [用户体验](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#ux)

        * [授予对照片和视频的部分访问权限](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#partial-photo-video-access)

        * [安全的全屏 intent 通知](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#secure-fsi)

        * [关于不可关闭通知用户体验方式的变更](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#non-dismissable-notifications)

        * [数据安全信息更显眼](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#data-safety)

    * [无障碍](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#accessibility)

        * [非线性字体放大至 200%](https://developer.android.google.cn/about/versions/14/behavior-changes-all?hl=zh-cn#non-linear-font-scaling)

* [针对 targetSdkVersion 34+ 应用的行为变更](https://developer.android.google.cn/about/versions/14/behavior-changes-14?hl=zh-cn)

    * [核心功能](https://developer.android.google.cn/about/versions/14/behavior-changes-14?hl=zh-cn#core)

        * [前台服务类型是必填项](https://developer.android.google.cn/about/versions/14/behavior-changes-14?hl=zh-cn#fgs-types)

        * [OpenJDK 17 更新](https://developer.android.google.cn/about/versions/14/behavior-changes-14?hl=zh-cn#core-libraries)

    * [安全](https://developer.android.google.cn/about/versions/14/behavior-changes-14?hl=zh-cn#security)

        * [对隐式 intent 和待处理 intent 的限制](https://developer.android.google.cn/about/versions/14/behavior-changes-14?hl=zh-cn#safer-intents)

        * [在运行时注册的广播接收器必须指定导出行为](https://developer.android.google.cn/about/versions/14/behavior-changes-14?hl=zh-cn#runtime-receivers-exported)

        * [更安全的动态代码加载](https://developer.android.google.cn/about/versions/14/behavior-changes-14?hl=zh-cn#safer-dynamic-code-loading)

        * [压缩路径遍历](https://developer.android.google.cn/about/versions/14/behavior-changes-14?hl=zh-cn#zip-path-traversal)

        * [针对从后台启动 activity 的其他限制](https://developer.android.google.cn/about/versions/14/behavior-changes-14?hl=zh-cn#background-activity-restrictions)

    * [更新后的非 SDK 限制](https://developer.android.google.cn/about/versions/14/behavior-changes-14?hl=zh-cn#non-sdk-restrictions)

#### 官方进度

* [Android 14 首个开发者预览版到来](https://mp.weixin.qq.com/s/xKjGv8EKQivcxAQiUMWIPA)

* [即刻体验 | Android 14 开发者预览版 2](https://mp.weixin.qq.com/s/JSzfpLQ_Wnm6t0JbX24Wjw)

* [Android 14 Beta 版发布，稳步提升与亮点并存](https://mp.weixin.qq.com/s/JolTdPhZqBwNl7_6INeiew)

* [丰富多彩 | Android 14 Beta 2 发布](https://mp.weixin.qq.com/s/JQyS_F8QBFdHbkMaRs91Uw)

* [平台稳定性里程碑 | Android 14 Beta 3 发布](https://mp.weixin.qq.com/s/l0IQXCg87lpQH3cT-QYrkA)

* [发布更新的好时机 | Android 14 Beta 4 发布](https://mp.weixin.qq.com/s/Rr9OqdLrFWBydikPE5sK6A)

* [正式版即将到来 | Android 14 Beta 5 发布](https://mp.weixin.qq.com/s/lmr5SBU80DeiOvL-lc68TA)

* [最新版发布 | Android 14 现已正式发布至 AOSP！](https://mp.weixin.qq.com/s/jIuGbttMVY4VxG6bTOddmQ)

#### 相关资源

* 适配简介

    * [Android 14 适配的那些事情](https://juejin.cn/post/7308434314777772042)

    * [Android 14 快速适配要点](https://juejin.cn/post/7231835495557890106)

    * [狂飙！Android 14 第一个预览版已发布～](https://juejin.cn/post/7198067983775973432)

    * [Android 14 又来了？别扶！抬起我来吧！](https://juejin.cn/post/7235906062309965880)

    * [深度解读 Android 14 重要的 8 个新特性～](http://juejin.cn/post/7249916242063802429)

    * [Android14 适配之——targetSdkVersion 升级到 34 需要注意些什么？](https://juejin.cn/post/7288964295697399843)

    * [Android 14 正式发布，已经在 AOSP 中上线，快来看看有什么吧](https://juejin.cn/post/728815171337396230)

    * [Android 14 的 8 个重要新特性深度解析](https://juejin.cn/post/7283361391671050240)

    * [Android14 适配之——现有 App 安装到 Android14 手机上需要注意些什么？](https://juejin.cn/post/7280747833384517687)

    * [卷起来，开始适配 Android 14](https://juejin.cn/post/7233208763921956920)

    * [Android 14(U) Gradle 8.x JDK 17 适配攻略](https://juejin.cn/post/7240690534074023973)

    * [Android 14 彻底终结大厂流氓应用](https://juejin.cn/post/7298699367791411236)

    * [Android 14 正式版适配笔记（一）— 针对所有应用的变更](https://juejin.cn/post/7299834584375869474)

    * [Android 14 正式版适配笔记（二）— 针对Android14或更高版本应用的变更](https://juejin.cn/post/7302348032544866316)

    * [Android14 应用兼容性问题报告](https://mp.weixin.qq.com/s/byB_Okpdq_9nbmdDoB3R3w)

* 厂商适配指南

    * [OPPO 开放平台 - Android 14 应用兼容性适配指导](https://open.oppomobile.com/new/developmentDoc/info?id=12262)

    * [VIVO 开放平台 - Android 14 开发者适配文档](https://dev.vivo.com.cn/documentCenter/doc/699)

    * [小米开放平台 - Android 14 应用适配指南](https://dev.mi.com/distribute/doc/details?pId=1718)

* 其他适配

    * [Android 14 权限适配方案](https://github.com/getActivity/XXPermissions)

    * [Android 14 新增权限](https://juejin.cn/post/7238762963908689957)

    * [Android 14 新 API：直接监听截屏操作，不用再观察媒体文件了～](https://juejin.cn/post/7219567168316473404)

    * [Android 14 新功能：区域偏好 Regional Preferences](https://juejin.cn/post/7248412998577782840)

    * [Android 14 新特性：语法性别 Grammatical Gender](https://juejin.cn/post/7245668131011182651)

    * [Android 14 之返回界面升级：预览目标界面 + 全新返回箭头](https://juejin.cn/post/7241125859729260600)

    * [Android 14 新功能之 TextView 搜索结果高亮和焦点移动](https://juejin.cn/post/7236680350558076983)

    * [Android 14 新功能之 HighLights：快速实现文本高亮～](https://juejin.cn/post/7214532871658291255)

    * [劝学：Android 14 Framework 引入了哪些“新”技术栈](https://juejin.cn/post/7231728952057249847)

    * [Android 14 前台服务适配指南](https://mp.weixin.qq.com/s/55a3uqbgfvOzPhmOyJvM6g)

    * [陪伴了 14 年的 API 下线了](https://juejin.cn/post/7303878037590442022)

## Android 13.0

#### 新特性

* [开发者工作效率和工具](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#developer-productivity)

    * [带主题的应用图标](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#themed-app-icons)

    * [各应用语言偏好设定](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#app-languages)

    * [改进了文本和语言支持](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#text-language)

    * [彩色矢量字体](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#color-vector-fonts)

    * [Quick Settings Placement API](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#quick-settings)

    * [剪贴板预览](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#copy-paste)

    * [预测性返回手势](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#predictive-back-nav)

    * [蓝牙 LE 音频](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#btle-audio)

    * [MIDI 2.0](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#midi-2-0)

    * [提高了启动画面效率](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#splash-screens)

* [隐私权和安全](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#privacy-security)

    * [更安全地导出上下文注册的接收器](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#runtime-receivers)

    * [照片选择器](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#photo-picker)

    * [针对附近 Wi-Fi 设备的新运行时权限](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#nearby-wifi-devices-permission)

    * [使用精确闹钟的新权限](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#use-exact-alarm-permission)

    * [开发者可降级权限](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#developer-downgradable-permissions)

    * [APK 签名方案 v3.1](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#apk-signature-scheme)

    * [改进了密钥库和 KeyMint 中的错误报告功能](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#keystore-keymint)

* [平板电脑和大屏设备支持](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#large-screens)

* [图形](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#graphics)

    * [可编程的着色器](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#shaders)

    * [改进了 Choreographer](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#choreographer)

* [媒体](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#media)

    * [预期音频路由](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#audio-routing)

* [无障碍功能](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#accessibility)

    * [语音描述](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#audio-description)

* [核心功能](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#core)

    * [OpenJDK 11 更新](https://developer.android.google.cn/about/versions/13/features?hl=zh-cn#core-libraries)

#### 行为更变

* [针对所有应用的行为变更](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn)

    * [性能和电池](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#performance-battery)

        * [前台服务 (FGS) 任务管理器](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#fgs-manager)

        * [使用 JobScheduler 改进预提取作业处理](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#prefetch-job-handling)

        * [电池资源利用率](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#battery-resource-utilization)

        * [高优先级 Firebase Cloud Message (FCM) 配额](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#fcm-quotas)

    * [隐私权](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#privacy)

        * [通知的运行时权限](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#notification-permission)

        * [从剪贴板中隐藏敏感内容](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#copy-sensitive-content)

    * [安全性](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#security)

        * [intent 过滤器会屏蔽不匹配的 intent](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#intents)

        * [停止使用共享用户 ID](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#shared-user-id)

    * [用户体验](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#ux)

        * [可以关闭前台服务通知](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#dismissible-fgs-notifs)

    * [核心功能](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#core)

        * [移除了旧版语音服务实现副本](https://developer.android.google.cn/about/versions/13/behavior-changes-all?hl=zh-cn#speech-service)

* [针对 targetSdkVersion 33+ 应用的行为变更](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn)

    * [隐私权](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#privacy)

        * [通知权限会影响前台服务的显示](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#notification-permission-fgs-appearance)

        * [针对附近 Wi-Fi 设备的新运行时权限](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#nearby-wifi-devices-permission)

        * [细化的媒体权限](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#granular-media-permissions)

        * [在后台使用身体传感器需要新的权限](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#body-sensors-background-permission)

    * [性能和电池](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#performance-battery)

        * [电池资源利用率](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#battery-resource-utilization)

    * [用户体验](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#ux)

        * [派生自 PlaybackState 的媒体控件](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#playback-controls)

        * [应用颜色主题会自动应用于 WebView 内容](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#webview-color-theme)

    * [Google Play 服务](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#gms)

        * [广告 ID 需要权限](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#ad-id)

    * [更新后的非 SDK 限制](https://developer.android.google.cn/about/versions/13/behavior-changes-13?hl=zh-cn#non-sdk-restrictions)

#### 官方进度

* [Android 13 首个开发者预览版到来](https://mp.weixin.qq.com/s/J_WPy9cFDcRCHslXz10rwA)

* [Android 13 Beta 版发布，诸多亮点不容错过](https://mp.weixin.qq.com/s/Y5CjnayCN1siimrDxwMbVg)

* [欢迎体验 | Android 13 开发者预览版 2](https://mp.weixin.qq.com/s/UVhWMl3mPSLB8nXNOZXuqQ)

* [平台稳定性里程碑 | Android 13 Beta 3 发布](https://mp.weixin.qq.com/s/2XnsMM7jS2IaXkcYWixV1w)

* [正式版即将到来 | Android 13 Beta 4 现已发布](https://mp.weixin.qq.com/s/_pGD_rySM2tYne4lJICmsA)

* [最新版发布 | Android 13 现已正式发布至 AOSP！](https://mp.weixin.qq.com/s/IYsoAjBBVnI36TluuennsQ)

#### 相关资源

* 适配简介

    * [Android 12 还没用上，Android 13 已经来了！](https://juejin.cn/post/7088605710728036359)

    * [Android 13 适配指南](https://juejin.cn/post/7099762078977622053)

    * [安卓13来了，快！扶起我来！](https://juejin.cn/post/7117449403765358605)

    * [Android 13 适配尝鲜](https://www.jianshu.com/p/e087c0d3b4a9)

    * [Android 13(T) 适配](https://www.jianshu.com/p/f0d390c2751e)

    * [Android 13 正式版发布](https://juejin.cn/post/7132720318736515085)

    * [移动开发前沿 | Android13，看这篇就够了！](https://mp.weixin.qq.com/s/ORYI1ALLfBw_OtjykJRoAA)

    * [个推解读 Android13，发布《Android13适配指南》](https://juejin.cn/post/7139772964639080485)

* 厂商适配指南

    * [OPPO 开放平台 - Android 13 应用兼容性适配指导](https://open.oppomobile.com/new/developmentDoc/info?id=11311)

    * [VIVO 开放平台 - Android 13 应用适配指南](https://dev.vivo.com.cn/documentCenter/doc/586)

    * [小米开放平台 - Android 13 应用适配指南](https://dev.mi.com/console/doc/detail?pId=2632)

* 其他适配

    * [Android 13 权限适配方案](https://github.com/getActivity/XXPermissions)

    * [Android 13 针对 Intent filters 安全的再加强](https://juejin.cn/post/7099450024525824037)

    * [Android 13 返回导航大变更：返回键彻底废弃 + 可预见型返回手势](https://juejin.cn/post/7105645114760331300)

    * [Android 13 新的换行策略和针对日文的优化](https://juejin.cn/post/7099054844404563982)

    * [前台服务管理器：如何手动在 Android 13 上「杀死」一个应用](https://neo.sspai.com/post/72283)

    * [Android 13 媒体权限适配指南](https://juejin.cn/post/7159999910748618766)

    * [微信 SDK - Android 13-可能存在的问题适配](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/Access_Guide/Android.html#jump3)

## Android 12.0 / 12L

#### 新特性

* [Android 12.0 新特性](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn)

	* [用户体验](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#experiences)
	
		* [Material You](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#material-you)
		
		* [微件改进](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#widgets)
		
		* [富媒体内容插入](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#unified-content-api)
		
		* [应用启动画面 API](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#splash-screen)
		
		* [圆角 API](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#rounded_corner_apis)
		
		* [富触感反馈体验](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#haptics)
		
		* [AppSearch](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#appsearch)
		
		* [游戏模式](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#gamemode)
		
		* [画中画 (PiP) 改进](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#pip-improvements)
		
		* [允许按来电重要性排名的新通话通知](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#new-calls)
		
		* [通知的丰富图片支持](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#enriched_image_support_for_notifications)
		
		* [沉浸模式下的手势导航改进](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#immersive-mode-improvements)
		
		* [近期网址共享（仅限 Pixel）](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#recents-url-sharing)
	
	* [安全和隐私设置](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#security-privacy)
	
		* [隐私信息中心](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#privacy-dashboard)
		
		* [蓝牙权限](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#bluetooth-permissions)
		
		* [权限组查找](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#permission-groups)
		
		* [隐藏应用叠加窗口](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#hide-application-overlay-windows)
		
		* [已知签名者权限保护标志](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#safer-grant-signature-perms)
		
		* [设备属性认证](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#device-properties-verification)
		
		* [安全锁定屏幕通知操作](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#notification-secure)
		
		* [BiometricPrompt 的可本地化字符串](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#biometric-prompt)
		
		* [即时通讯应用中的钓鱼式攻击检测功能（仅限 Pixel）](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#pixel-phishing-detection)
	
	* [媒体](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#media)
	
		* [兼容的媒体转码](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#transcoding)
		
		* [性能等级](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#performance-class)
		
		* [视频编码改进](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#video-encoding)
		
		* [音频焦点](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#audio-focus)
		
		* [MediaDrm 更新](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#mediadrm)
	
	* [相机](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#camera)
	
		* [Camera2 供应商扩展](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#camera2-extensions)
		
		* [Quad Bayer 摄像头传感器支持](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#camera-sensor-support)
	
	* [图形和图片](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#graphics)
	
		* [让应用能够直接访问 Tombstone 跟踪记录](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#provide_apps_direct_access_to_tombstone_traces)
		
		* [AVIF 图片支持](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#avif)
		
		* [更简单的模糊处理、颜色滤镜及其他效果](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#rendereffect)
		
		* [原生动画图片解码](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#image-decoder)
	
	* [连接性](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#connectivity)
	
		* [使配套应用保持唤醒状态](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#keep-awake)
		
		* [配套设备管理器配置文件](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#cdm-profiles)
		
		* [带宽估测改进](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#bandwidth-estimation)
		
		* [Wi-Fi 感知 (NAN) 增强功能](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#wifi-aware-enhancements)
		
		* [并发点对点 + 互联网连接](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#concurrent-connections)
		
		* [为 NFC 付款启用屏幕关闭](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#screen-on-nfc)
	
	* [存储](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#storage)
	
	* [核心功能](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#core)
	
		* [自动更新应用](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#automatic-app-updates)
		
		* [设备芯片组信息](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#soc-info)
		
		* [核心 Java API 的更新](https://developer.android.google.cn/about/versions/12/features?hl=zh-cn#java-api)

	* [微件改进](https://developer.android.google.cn/about/versions/12/features/widgets?hl=zh-cn)

	* [企业版的新变化](https://developer.android.google.cn/about/versions/12/work?hl=zh-cn)

* [Android 12L 功能和变更](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn)

    * [针对大屏设备优化了操作系统](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#system-ui)
    
        * [面向开发者：媒体投影的变化](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#media-projection,)
    
    * [强大直观的多任务处理功能](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#multitasking)
    
        * [面向开发者：在分屏模式下测试应用](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#dev-test-splitscreen,)
    
    * [改善了兼容性体验](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#compatibility)
    
        * [面向开发者：在兼容模式下检查应用](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#dev-check-compat,)
    
    * [针对大屏设备的更多更新和资源](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#more-updates)
    
        * [大屏设备上 Google Play 的变化](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#google-play,)
    
        * [使用 Jetpack WindowManager 嵌入 activity](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#dev-activity-embedding,)
    
        * [设备屏幕方向请求](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#dev-device-orientation-request,)
    
    * [让您的应用做好准备](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#get-apps-ready)
    
        * [要测试的内容](https://developer.android.google.cn/about/versions/12/12L/summary?hl=zh-cn#what-to-test)

#### 行为变更

* [针对所有应用的行为变更](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn)

    * [用户体验](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#user_experience)

        * [滚动效果](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#overscroll)

        * [前台服务通知用户体验延迟](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#foreground-service-notification-delay)

        * [沉浸模式下的手势导航改进](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#immersive-mode-improvements)

        * [网络 intent 解析](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#web-intent-resolution)

        * [限制性应用待机模式存储分区](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#restrictive-app-standby-bucket)

        * [Display#getRealSize 和 getRealMetrics：废弃和沙盒](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#displaymetrics)

    * [图形和图片](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#graphics)

        * [改进了刷新率切换](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#refresh-rate)

    * [安全和隐私设置](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#security-privacy)

        * [麦克风和摄像头切换开关](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#mic-camera-toggles)

        * [麦克风和摄像头指示标志](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#mic-camera-indicators)

        * [应用无法关闭系统对话框](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#close-system-dialogs)

        * [不受信任的触摸事件被屏蔽](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#untrusted-touch-events)

        * [权限软件包可见性](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#permission-package-visibility)

        * [移除了 Bouncy Castle 实现](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#bouncy-castle)

        * [剪贴板访问通知](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#clipboard-access-notifications)

    * [连接性](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#connectivity)

        * [Passpoint 更新](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#passpoint-updates)

    * [更新后的非 SDK 接口限制](https://developer.android.google.cn/about/versions/12/behavior-changes-all?hl=zh-cn#non-sdk-restrictions)

* [针对 targetSdkVersion 31+ 应用的行为变更](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn)

    * [用户体验](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#ux)

        * [画中画行为改进](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#pip-behavior-improvements)

        * [自定义通知](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#custom-notifications)

        * [Android App Links 验证的变更](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#android-app-links-verification-changes)

    * [隐私设置](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#privacy)

        * [大致位置](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#approximate-location)

        * [应用休眠](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#app-hibernation)

        * [移动传感器有采样率限制](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#motion-sensor-rate-limiting)

        * [数据访问审核](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#data-access-auditing)

        * [WebView 中的现代 SameSite Cookie](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#samesite)

        * [ADB 备份限制](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#adb-backup-restrictions)

    * [安全](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#security)

        * [更安全的组件导出](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#exported)

        * [尽可能创建不可变的待处理 intent](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#create-immutable-pending-intents)

        * [不安全的 intent 启动](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#unsafe-intent-launches)

    * [性能](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#performance)

        * [前台服务启动限制](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#foreground-service-launch-restrictions)

        * [精确的闹钟权限](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#exact-alarm-permission)

        * [通知 trampoline 限制](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#notification-trampolines)

    * [备份和恢复](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#backup-restore)

    * [连接性](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#connectivity)

        * [并发点对点 + 互联网连接](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#concurrent-connections)

        * [为 NFC 付款启用屏幕关闭](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#screen-on-nfc)

    * [供应商库](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#vendor-libraries)

        * [供应商提供的原生共享库](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#uses-native-library)

    * [更新后的非 SDK 限制](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#vendor-libraries)

#### 官方进度

* [一起看 I/O | Android 12 Beta 版发布，诸多亮点不容错过](https://mp.weixin.qq.com/s/_KlPUqNoJTfO3C8igPG49w)

* [更进一步 | Android 12 Beta 2 发布](https://mp.weixin.qq.com/s/yygBn-cOrX4d4Wqs70CeDg)

* [终版 API 正式到来 | Android 12 Beta 3 发布](https://mp.weixin.qq.com/s/-SqSiGm9srvVyBa3dVbpsg)

* [平台稳定性里程碑 | Android 12 Beta 4 现已发布](https://mp.weixin.qq.com/s/phUf11X59EEH_oDqzmfNzg)

* [正式版即将到来 | Android 12 Beta 5 现已发布](https://mp.weixin.qq.com/s/eEPwTzIfzPKRXD31o72IrQ)

* [Android 12 正式发布 | 开发者们的全新舞台](https://mp.weixin.qq.com/s/OiFSWEnc-0N2z7JYWTJluw)

* [新版本系统适配: Android 12 中的兼容性变更](https://mp.weixin.qq.com/s/OiFSWEnc-0N2z7JYWTJluw)

#### 相关资源

* 适配简介

    * [Android 12 适配简介](https://juejin.cn/post/7014491424112508936)

    * [Android 12 快速适配要点](https://juejin.cn/post/7037105000480243748)

    * [来了！Android 12 适配你准备好了吗？](https://juejin.cn/post/7031411081457336357)

    * [还没适配 Android 12 的要抓紧了](https://juejin.cn/post/7088731887945908260)

    * [TargetsdkVersion 升级 31（Android12）适配](https://www.jianshu.com/p/ec1b3295b271)

    * [Android 12 保姆级适配指南](https://juejin.cn/post/7093787313095999502)

    * [Android Target 31 升级全攻略 —— 记阿里首个超级 App 的坎坷升级之路](https://juejin.cn/post/7114225231845457956)

    * [Android 12 适配-行为变更：所有应用](https://www.jianshu.com/p/76263c20df47)

    * [Android 12 适配-行为变更：以 Android 12 为目标平台的应用](https://www.jianshu.com/p/af3d9baa9156)

    * [您有一份安卓 12 适配攻略，请注意查收！](https://mp.weixin.qq.com/s/vyKVaIGQHrisuuA8tT317w)

* 厂商适配指南

    * [OPPO 开放平台 - Android 12 应用兼容性适配指导](https://open.oppomobile.com/wiki/doc#id=10960)

    * [VIVO 开放平台 - Android 12 应用适配指南](https://dev.vivo.com.cn/documentCenter/doc/509)

    * [小米开放平台 - Android 12 应用适配指南](https://dev.mi.com/console/doc/detail?pId=2439)

* SplashScreen 适配

    * [从 Jetpack SplashScreen 深度探讨 App 启动画面的前世今生～](https://juejin.cn/post/7044713406774902820)

    * [Jetpack 新成员 SplashScreen：打造全新的App启动画面](https://juejin.cn/post/6997217571208445965)

    * [Android 12 SplashScreen API 快速入门](https://guolin.blog.csdn.net/article/details/120275319)

    * [Jetpack SplashScreen API 在所有 Android 系统上使用总结，内含原理分析](https://juejin.cn/post/7019839767441309733)

    * [Android 12 启动画面-SplashScreen](https://juejin.cn/post/7026188311198695432)

    * [Android 12 上全新的应用启动画面，还不适配一下？](https://juejin.cn/post/6962706834889113614)

    * [用 SplashScreen 做一个会动的开屏！](https://juejin.cn/post/7150692699350237191)

    * [Android SplashScreen API：打造引人注目的启动画面](https://mp.weixin.qq.com/s/pb9N22AGF6mWtpjWS3q_IQ)

* 桌面小组件适配

    * [更新您的 widget 以适配 Android 12](https://www.jianshu.com/p/8dade210fcfd)

    * [Android 12 上焕然一新的小组件：美观、便捷和实用](https://juejin.cn/post/6968851189190377480)

    * [别羡慕苹果的小部件了，安卓也有！](https://juejin.cn/post/7037303315595526157)

* exported 属性适配

    * [Android 12 新特性 android:exported 属性](https://www.jianshu.com/p/89dc6c109834)

    * [Android 12 自动适配 exported 深入解析避坑](https://juejin.cn/post/7074018771161219103)

    * [写了一个适配 Android12-exported 的小插件](https://juejin.cn/post/7113738206318690340)

    * [The application could not be installed: `INSTALL_PARSE_FAILED_MANIFEST_MALFORMED`](https://developer.android.google.cn/about/versions/12/behavior-changes-12?hl=zh-cn#exported)

* Android 12 L 适配

    * [详解 Android 12L｜更好地适配大屏幕设备](https://mp.weixin.qq.com/s/NN0CzWoKfIALPZbHjWQk5Q)

    * [正式版 API 确定 | Android 12L Beta 1 发布](https://mp.weixin.qq.com/s/G6UEensT8J4ZWDuSGYTwNA)

    * [Android 与 Chrome OS 中针对大屏幕设备的更新](https://mp.weixin.qq.com/s/F5Jk-nVjeHOUe5qiSIEE3A)

* 其他适配

    * [Android 12 蓝牙适配攻略](https://llw-study.blog.csdn.net/article/details/124420936)

    * [Android 12 蓝牙权限适配方案](https://github.com/getActivity/XXPermissions)

    * [Android 12 实用更新：置灰的控件也可以点击啦](https://juejin.cn/post/7100916142776008740)

    * [Android 12 TransactionTooLargeException 问题](https://juejin.cn/post/7125729625442877448)

    * [高德地图 - Android 12 定位权限说明](https://lbs.amap.com/api/android-location-sdk/guide/utilities/permision_12)

    * [百度地图 - Android 12.0 开发须知](https://lbs.baidu.com/index.php?title=android-locsdk/guide/addition-func/android12-notice)

    * [支持Android 12，全版本保存图片到相册方案](https://juejin.cn/post/7042218651482587172)

## Android 11.0

#### 概览

| 隐私权变更 | 受影响的应用 | 缓解策略 |
| :---: | :---------: | :------: |
| **强制执行分区存储机制** 以 Android 11 或更高版本为目标平台的应用始终会受分区存储行为的影响 | 以 Android 11 或更高版本为目标平台的应用，以及以 Android 10 为目标平台且未将 `requestLegacyExternalStorage` 设为 `true` 以停用分区存储的应用 | 更新您的应用以使用分区存储 [详细了解分区存储变更](https://developer.android.google.cn/about/versions/11/privacy/storage?hl=zh-cn) |
| **单次授权** 使用单次授权功能，用户可以授予对位置信息、麦克风和摄像头的临时访问权限 | 在 Android 11 或更高版本上运行且请求位置信息、麦克风或摄像头权限的应用 | 在尝试访问受某项权限保护的数据之前，检查您的应用是否具有该权限 [遵循请求权限方面的最佳做法](https://developer.android.google.cn/training/permissions/requesting?hl=zh-cn) |
| **自动重置权限** 如果用户在 Android 11 或更高版本上几个月未与应用互动，系统会自动重置应用的敏感权限 | 以 Android 11 或更高版本为目标平台且在后台执行大部分工作的应用 | 要求用户阻止系统重置应用的权限 [详细了解自动重置权限](https://developer.android.google.cn/about/versions/11/privacy/permissions?hl=zh-cn#auto-reset) |
| **后台位置信息访问权限** Android 11 更改了用户向应用授予后台位置信息权限的方式 | 以 Android 11 或更高版本为目标平台且需要[在后台访问位置信息](https://developer.android.google.cn/training/location/permissions?hl=zh-cn#background)的应用 | 通过对权限请求方法的多次单独调用，逐步请求在前台（粗略或精确）和后台访问位置信息的权限。必要时，说明用户授予该权限所能得到的益处 [详细了解 Android 11 中的在后台访问位置信息的权限](https://developer.android.google.cn/about/versions/11/privacy/location?hl=zh-cn#background-location) |
| **软件包可见性** Android 11 更改了应用查询同一设备上的其他已安装应用及与之互动的方式 | 以 Android 11 或更高版本为目标平台且与设备上的其他已安装应用交互的应用 | 将 `<queries>` 元素添加到应用的清单 [详细了解软件包可见性](https://developer.android.google.cn/about/versions/11/privacy/package-visibility?hl=zh-cn) |
| **前台服务** Android 11 更改了前台服务访问位置信息、摄像头和麦克风相关数据的方式 | 在 Android 11 或更高版本上运行且在前台服务中访问位置信息、摄像头或麦克风的应用 | 分别针对需要访问摄像头和麦克风的前台服务，声明 `camera` 和 `microphone` 前台服务类型。但请注意，应用在后台运行时启动的前台服务通常无法访问位置信息、摄像头或麦克风。 [详细了解前台服务的变更](https://developer.android.google.cn/about/versions/11/privacy/foreground-services?hl=zh-cn) |

#### 新特性

* [向您的应用添加 5G 功能](https://developer.android.google.cn/about/versions/11/features/5g?hl=zh-cn)

* [强制门户 API 支持](https://developer.android.google.cn/about/versions/11/features/captive-portal?hl=zh-cn)

* [安全共享大型数据集](https://developer.android.google.cn/training/data-storage/shared/datasets?hl=zh-cn)

* [联系人与对话](https://developer.android.google.cn/guide/topics/ui/conversations?hl=zh-cn)

* [消息框](https://developer.android.google.cn/preview/features/toasts)

* [控制外部设备](https://developer.android.google.cn/guide/topics/ui/device-control?hl=zh-cn)

* [将自动填充功能与键盘集成](https://developer.android.google.cn/guide/topics/text/ime-autofill?hl=zh-cn)

#### 行为更变

* [针对所有应用的行为变更](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn)

    * [隐私权](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#privacy)

        * [单次授权](https://developer.android.google.cn/about/versions/11/privacy/permissions?hl=zh-cn#one-time)

        * [权限对话框的可见性](https://developer.android.google.cn/about/versions/11/privacy/permissions?hl=zh-cn#dialog-visibility)

        * [数据访问审核](https://developer.android.google.cn/about/versions/11/privacy/data-access-auditing?hl=zh-cn)

        * [系统提醒窗口权限](https://developer.android.google.cn/about/versions/11/privacy/permissions?hl=zh-cn#system-alert)

        * [永久 SIM 卡标识符](https://developer.android.google.cn/training/articles/user-data-ids?hl=zh-cn#mobile-service-subscriptions)

    * [接触史通知](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#exposure-notifications)
    
    * [安全性](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#security)
    
        * [SSL 套接字默认情况下使用 Conscrypt SSL 引擎](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#ssl-sockets-conscrypt)
    
        * [Scudo Hardened Allocator](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#scudo)
    
        * [应用使用情况统计信息](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#app-usage-stats)
    
        * [针对 5G 的模拟器支持](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#emulator-5g)
    
    * [性能和调试](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#perf-debug)
    
        * [JobScheduler API 调用限制调试](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#jobscheduler_quotas)
    
        * [文件描述符排错程序 (fdsan)](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#fdsan)
    
    * [非 SDK 接口限制](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#non-sdk-restrictions)
    
    * [V1 版 Google 地图共享库已移除](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#maps-v1-removed)
    
    * [与其他应用交互](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#interaction-other-apps)
    
        * [分享内容 URI](https://developer.android.google.cn/about/versions/11/behavior-changes-all?hl=zh-cn#share-content-uris)

* [针对 targetSdkVersion 30+ 应用的行为变更](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn)

    * [隐私权](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#privacy)

        * [强制执行分区存储](https://developer.android.google.cn/about/versions/11/privacy/storage?hl=zh-cn#scoped-storage)

        * [自动重置权限](https://developer.android.google.cn/about/versions/11/privacy/permissions?hl=zh-cn#auto-reset)

        * [在后台访问位置信息的权限](https://developer.android.google.cn/about/versions/11/privacy/location?hl=zh-cn#background-location)

        * [软件包可见性](https://developer.android.google.cn/about/versions/11/privacy/package-visibility?hl=zh-cn)

    * [安全](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#security)
    
        * [堆指针标记](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#heap-pointer-tagging)
    
        * [消息框的更新](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#toasts)
    
    * [网络连接](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#connectivity)
    
        * [限制对 APN 数据库的读取访问](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#apn-database-restrictions)
    
    * [无障碍服务](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#accessibility)
    
        * [在清单文件中声明与 TTS 引擎的交互](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#tts-engines)
    
        * [在元数据文件中声明“无障碍”按钮使用情况](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#a11y-button-usage)
    
    * [相机](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#camera)
    
        * [媒体 intent 操作需要系统默认相机](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#media-capture)
    
    * [应用打包和安装](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#app-packaging)
    
        * [压缩的资源文件](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#compressed-resource-file)
    
        * [现在需要 APK 签名方案 v2](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#minimum-signature-scheme)
    
    * [Firebase](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#firebase)
    
        * [Firebase JobDispatcher 和 GCMNetworkManager](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#gcmnm)
    
    * [设备到设备文件传输](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#device-to-device-file-transfer)
    
    * [OnSharedPreferenceChangeListener 的回调变更](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#sharedpreferences-listener)
    
    * [非 SDK 接口限制](https://developer.android.google.cn/about/versions/11/behavior-changes-11?hl=zh-cn#non-sdk-restrictions)

#### 相关资源

* 适配简介

    * [Android 11 开发者手册](android_11_dev_booklet.pdf)

    * [拖不得了，Android11真的要来了，最全适配实践指南奉上](https://juejin.im/post/6860370635664261128)

    * [Android 11 变更及适配攻略](https://juejin.cn/post/6948211914455384072)

    * [实战 Android 升级目标版本到 30 过程中遇到的问题及解决办法](https://juejin.cn/post/7031128042843930655)

* 厂商适配指南

    * [OPPO 开放平台 - Android 11 应用兼容性适配指导](https://open.oppomobile.com/wiki/doc#id=10724)

    * [VIVO 开放平台 - Android 11 应用适配指南](https://dev.vivo.com.cn/documentCenter/doc/428)

    * [小米开放平台 - Android 11上第三方App读写文件API标准建议](https://dev.mi.com/console/doc/detail?pId=2323)

* Android/data 目录适配

    * [Android 11 无 Root 访问 data 目录实现、Android 11 访问 data 目录、Android 11 解除 data 目录限制、Android 11 data 空白解决](https://blog.csdn.net/qq_17827627/article/details/113931692)

    * [知乎回答：如何评价在 Android11 中，/Android/data 文件夹无法读写？](https://www.zhihu.com/question/420023759)

    * [Android 11 适配- 实现清理其他应用缓存目录](https://blog.csdn.net/u013700040/article/details/115066778)

* 其他适配

    * [Android 11 外部存储权限适配指南及方案](https://www.jianshu.com/p/e94cea26e213)

    * [Android 11 绕过反射限制](https://www.jianshu.com/p/6546ce67c8e0)

    * [Android 11 软件包可见性适配](https://www.jianshu.com/p/d1ccd425c4ce)

    * [Android 11 特性调整：安装外部来源应用需要重启APP](https://cloud.tencent.com/developer/news/637591)

    * [Android 11 无法在后台显示自定义样式 Toast 的适配方案](https://github.com/getActivity/Toaster)

    * [微信开放平台 - Android 11 系统策略更新](https://open.weixin.qq.com/cgi-bin/announce?action=getannouncement&key=11600155960jI9EY&version=&lang=&token=)

    * [文本转语音 TTS 开发 Android11 适配方案](https://www.jianshu.com/p/d1767a397c10)

## Android 10.0

#### 概览

|      隐私权变更     |       受影响的应用  |    缓解策略      | 
| :---------: | :---------------: | :--------------: | 
| **分区存储** 针对外部存储的过滤视图，可提供对特定于应用的文件和媒体集合的访问权限 | 访问和共享外部存储中的文件的应用     | 使用特定于应用的目录和媒体集合目录 [了解详情](https://developer.android.google.cn/about/versions/10/privacy/changes?hl=zh-cn#scoped-storage) |
| **增强了用户对位置权限的控制力** 仅限前台权限，可让用户更好地控制应用对设备位置信息的访问权限 | 在后台时请求访问用户位置信息的应用   | 确保在没有后台位置信息更新的情况下优雅降级 使用 Android 10 中引入的权限在后台获取位置信息 [了解详情](https://developer.android.google.cn/about/versions/10/privacy/changes?hl=zh-cn#app-access-device-location) |
| **系统执行后台 Activity** 针对从后台启动 Activity 实施了限制 | 不需要用户互动就启动 Activity 的应用 | 使用通知触发的 Activity [了解详情](https://developer.android.google.cn/about/versions/10/privacy/changes?hl=zh-cn#background-activity-starts) |
| **不可重置的硬件标识符** 针对访问设备序列号和 IMEI 实施了限制 | 访问设备序列号或 IMEI 的应用         | 使用用户可以重置的标识符 [了解详情](https://developer.android.google.cn/about/versions/10/privacy/changes?hl=zh-cn#non-resettable-device-ids) |
| **无线扫描权限** 访问某些 WLAN、WLAN 感知和蓝牙扫描方法需要获得精确位置权限 | 使用 WLAN API 和蓝牙 API 的应用      | 针对相关使用场景请求 `ACCESS_FINE_LOCATION` 权限 [了解详情](https://developer.android.google.cn/about/versions/10/privacy/changes?hl=zh-cn#location-telephony-bluetooth-wifi) |

#### 新特性

* [折叠屏](https://developer.android.google.cn/about/versions/10/highlights?hl=zh-cn#foldables)

* [5G 网络](https://developer.android.google.cn/about/versions/10/highlights?hl=zh-cn#5g_networks)

* [通知栏消息回复](https://developer.android.google.cn/about/versions/10/highlights?hl=zh-cn#smart_reply_in_notifications)

* [深色主题](https://developer.android.google.cn/about/versions/10/highlights?hl=zh-cn#dark_theme)

* [手势导航](https://developer.android.google.cn/about/versions/10/highlights?hl=zh-cn#gesture_navigation)

* [设置面板](https://developer.android.google.cn/about/versions/10/highlights?hl=zh-cn#settings_panels)

* [共享快捷方式](https://developer.android.google.cn/about/versions/10/highlights?hl=zh-cn#sharing_shortcuts)

#### 行为更变

* [针对所有应用的行为变更](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn)

    * [限制非 SDK 接口](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#non-sdk-restrictions)
    
    * [手势导航](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#gesture-nav)
    
    * [NDK](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#q-ndk)
    
        * [共享对象不得包含文本重定位](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#textrel)
    
    * [Bionic 库和动态链接器路径变更](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#bionic)
    
    * [系统二进制文件/库会映射到只执行内存](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#xom-binaries)
    
    * [安全](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#security)
    
        * [TLS 1.3 默认处于启用状态](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#tls-1.3)
    
        * [TLS 不信任使用 SHA-1 签名的证书](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#sha1-not-trusted)
    
        * [KeyChain 行为变更和改进](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#keychain)
    
        * [其他 TLS 和加密更改](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#tls-crypto)
    
    * [WLAN 直连广播](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#wifi-direct-broadcasts)
    
    * [WLAN 感知功能](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#wifi-aware)
    
    * [Go 设备上的 `SYSTEM_ALERT_WINDOW`](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#sysalert-go)
    
    * [关于以旧版 Android 系统为目标平台的应用的警告](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#low-target-sdk-warnings)
    
    * [移除了 SHA-2 CBC 加密套件](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#sha2-cbc-cipher-suites)
    
    * [应用使用情况](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#app-usage)
    
    * [HTTPS 连接变更](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#https-connection)
    
    * [ZIP 文件实用程序库变更](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#zip-file-library)
    
        * [Inflater](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#inflater)
    
        * [ZipFile](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#zip-file)
    
        * [ZipOutputStream](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#zip-output-stream)
        
    * [摄像头变更](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#camera)
    
    * [电池用量跟踪](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#battery-tracking)
    
    * [Android Beam 已弃用](https://developer.android.google.cn/about/versions/10/behavior-changes-all?hl=zh-cn#beam-deprecation)

* [针对 targetSdkVersion 29+ 应用的行为变更](https://developer.android.google.cn/about/versions/10/behavior-changes-10?hl=zh-cn)

    * [有关限制非 SDK 接口的更新](https://developer.android.google.cn/about/versions/10/behavior-changes-10?hl=zh-cn#non-sdk-restrictions)
    
    * [共享内存](https://developer.android.google.cn/about/versions/10/behavior-changes-10?hl=zh-cn#shared-memory)
    
    * [移除了应用主目录的执行权限](https://developer.android.google.cn/about/versions/10/behavior-changes-10?hl=zh-cn#execute-permission)
    
    * [Android 运行时只接受系统生成的 OAT 文件](https://developer.android.google.cn/about/versions/10/behavior-changes-10?hl=zh-cn#system-only-oat)
    
    * [在 ART 中强制要求 AOT 正确性](https://developer.android.google.cn/about/versions/10/behavior-changes-10?hl=zh-cn#aot)
    
    * [针对全屏 Intent 的权限变更](https://developer.android.google.cn/about/versions/10/behavior-changes-10?hl=zh-cn#full-screen-intents)
    
    * [支持可折叠设备](https://developer.android.google.cn/about/versions/10/behavior-changes-10?hl=zh-cn#foldables)
    
    * [java.io.FileChannel.map() 更改](https://developer.android.google.cn/about/versions/10/behavior-changes-10?hl=zh-cn#filechannel-map)

#### 相关资源

* 适配简介

   * [Android 10 适配攻略](https://juejin.cn/post/6844904073024503822)

* 厂商适配指南

    * [OPPO 开放平台 - Android Q 版本应用兼容性适配指导](https://open.oppomobile.com/new/developmentDoc/info?id=10432)

    * [VIVO 开放平台 - Android Q 应用适配指南](https://dev.vivo.com.cn/documentCenter/doc/235)

* 分区存储适配

   * [暂时停用分区存储](https://developer.android.google.cn/training/data-storage/use-cases#opt-out-scoped-storage)

   * [Android 存储用例和最佳做法](https://developer.android.google.cn/training/data-storage/use-cases)

   * [Android 10(Q)/11(R) 分区存储适配](https://juejin.cn/post/6862633674089693197)

   * [Android 10 分区存储适配](https://www.jianshu.com/p/37feb5116191)

   * [Android 10 适配要点，作用域存储](https://blog.csdn.net/guolin_blog/article/details/105419420)

   * [Android MediaStore Api 使用](https://ppting.me/2020/04/19/2020_04_19_how_to_use_Android_MediaStore_Api/)

   * [QQ SDK - 分区存储功能适配](https://wiki.connect.qq.com/%e5%88%86%e4%ba%ab%e5%8a%9f%e8%83%bd%e5%ad%98%e5%82%a8%e6%9d%83%e9%99%90%e9%80%82%e9%85%8d)

   * [微信 SDK - 分区存储功能适配](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/Access_Guide/Android.html#jump2)

   * [支持Android 12，全版本保存图片到相册方案](https://juejin.cn/post/7042218651482587172)

* 深色主题适配

   * [Android 深色模式适配原理分析](https://www.jianshu.com/p/1aaf0cee7a2f)

   * [Android 10 适配要点，深色主题](https://guolin.blog.csdn.net/article/details/106061657)

   * [Android 深色模式的项目应用](https://juejin.cn/post/7022270811524300808)

   * [Android 10 暗黑模式适配，你需要知道的一切](https://juejin.cn/post/6844904173788463112)

* 其他适配

   * [Android 折叠屏适配攻略](https://juejin.cn/post/6844903889267867656)

   * [Android 监听系统截屏操作，适配Android Q（29）](https://juejin.cn/post/7189126960319037495) 

## Android 9.0

#### 新特性

* [利用 Wi-Fi RTT 进行室内定位](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#rtt)

* [显示屏缺口支持](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#cutout)

* [通知](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#notifications)

* [多摄像头支持和摄像头更新](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#camera)

* [适用于可绘制对象和位图的 ImageDecoder](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#decoding-images)

* [动画](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#animation)

* [HDR VP9 视频、HEIF 图像压缩和 Media API](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#hdr_vp9_%E8%A7%86%E9%A2%91%E3%80%81heif_%E5%9B%BE%E5%83%8F%E5%8E%8B%E7%BC%A9%E5%92%8C_media_api)

* [JobScheduler 中的流量费用敏感度](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#jobscheduler)

* [Neural Networks API 1.1](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#nnapi)

* [自动填充框架](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#autofill)

* [安全增强功能](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#security)

* [Android 备份](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#android-backups)

* [无障碍功能](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#a11y)

* [旋转](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#rotation)

* [文本](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#text)

* [设备端系统跟踪](https://developer.android.google.cn/about/versions/pie/android-9.0?hl=zh-cn#on-device-systrace)

#### 行为更变

* [针对所有应用的行为变更](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn)

    * [电源管理](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#power)

    * [隐私权变更](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#privacy-changes-all)

    * [对使用非 SDK 接口的限制](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#compat)

    * [安全行为变更](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#security-changes)

        * [设备安全性变更](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#device-security-changes)

    * [ICU 库更新](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#icu)

    * [Android Test 变更](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#android-test-changes)

    * [Java UTF 解码器](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#decoder)

    * [使用证书的主机名验证](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#certificate-common-name)

    * [网络地址查询可能会导致网络违规](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#network-address-strictmode)

    * [套接字标记](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#trafficstats-setthreadstatstag)

    * [报告的套接字中可用字节数](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#socketimpl-shutdowninput)

    * [应用不再能访问 `xt_qtaguid` 文件夹中的文件](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#qtaguid-nolonger-accessible)

    * [现在强制执行 `FLAG_ACTIVITY_NEW_TASK` 要求](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#fant-required)

    * [屏幕旋转变更](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#screen-rotation-changes)

    * [Apache HTTP 客户端弃用影响采用非标准 ClassLoader 的应用](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#trafficstats-setthreadstatstag)

    * [枚举相机](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-all?hl=zh-cn#multi-camera)
    
* [针对 targetSdkVersion 28+ 应用的行为变更](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn)

    * [前台服务](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#fg-svc)
    
    * [隐私权变更](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#privacy-changes-p)
    
    * [框架安全性变更](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#framework-security-changes)

        * [默认启用网络传输层安全协议 (TLS)](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#tls-enabled)
    
        * [按进程分设基于网络的数据目录](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#web-data-dirs)

    * [网络连接变更](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#connectivity-changes)
    
        * [网络连接数据计数和多路径](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#data-counting-multipath)
    
        * [Apache HTTP 客户端弃用](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#apache-p)
    
    * [界面变更](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#ui-changes)
    
        * [视图焦点](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#focus)
    
        * [CSS RGBA 十六进制值处理](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#hex-value-handling)
    
        * [文件的 MIME 类型嗅探：URI](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#mime-type-sniffing)
    
        * [文档滚动元素](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#scrolling-element)
    
        * [来自已暂停应用的通知](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28?hl=zh-cn#suspended-apps)

#### 相关资源

* 适配简介

    * [Android 9.0 适配指南](https://juejin.cn/post/6844903906942648334)

    * [Android 9.0适配及部分新特性介绍](https://cloud.tencent.com/developer/article/1370376)

* 厂商适配指南

    * [VIVO 开放平台 - Android P 应用适配指南](https://dev.vivo.com.cn/documentCenter/doc/145)

    * [小米开放平台 - MIUI Android P 适配指南](https://dev.mi.com/console/doc/detail?pId=1351)

* 刘海屏适配

    * [Android 刘海屏适配全攻略](https://www.jianshu.com/p/561f7241153b)

    * [Android 9.0 系统新特性，对刘海屏设备进行适配](https://guolin.blog.csdn.net/article/details/103112795)

    * [Android 刘海屏适配框架（停止维护）](https://github.com/zhangzhun132/NotchTools)

* 反射 API 适配

    * [区分 SDK 接口和非 SDK 接口](https://developer.android.google.cn/guide/app-compatibility/restrictions-non-sdk-interfaces?hl=zh-cn)

    * [一种绕过 Android P 对非 SDK 接口限制的简单方法](https://weishu.me/2018/06/07/free-reflection-above-android-p)

    * [另一种绕过 Android P 以上非公开 API 限制的办法](https://weishu.me/2019/03/16/another-free-reflection-above-android-p)

    * [隐藏 API 反射框架 FreeReflection](https://github.com/tiann/FreeReflection)

* WebView 多进程适配

    * [Android 9.0/P WebView 多进程使用的问题](https://www.cnblogs.com/renhui/p/13942060.html)

    * [有效解决 WebView 多进程崩溃](https://juejin.cn/post/6942298361454133261)

## Android 8.0 / 8.1

#### 新特性

* [Android 8.0 新特性](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn)

    * [用户体验](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#ux)

        * [通知](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#notifications)
    
        * [自动填充框架](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#af)
    
        * [画中画模式](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#opip)
    
        * [可下载字体](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#df)
    
        * [XML 中的字体](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#fix)
    
        * [自动调整 TextView 的大小](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#atv)
    
        * [自适应图标](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#ai)
    
        * [颜色管理](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#cm)
    
        * [WebView API](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#wv)
    
        * [固定快捷方式和小部件](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#iapoas)
    
        * [最大屏幕纵横比](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#max-aspect-ratio)
    
        * [多显示器支持](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#mds)
    
        * [统一的布局外边距和内边距](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#ulmp)
    
        * [指针捕获](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#pc)
    
        * [应用类别](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#category)
    
        * [Android TV 启动器](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#tvlauncher)
    
        * [AnimatorSet](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#aset)
    
        * [输入和导航](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#ian)
    
    * [系统](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#sys)

        * [视图默认焦点](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#vdf)
    
        * [新的 StrictMode 检测程序](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#strictmode)
    
        * [缓存数据](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#cache)
    
        * [内容提供程序分页](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#cpp)
    
        * [内容刷新请求](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#df)
    
        * [JobScheduler 改进](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#jobscheduler)
    
        * [自定义数据存储](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#data-store)
    
        * [findViewById 签名变更](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#fvbi-signature)
    
    * [媒体增强功能](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#me)

        * [VolumeShaper](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#media-vs)
    
        * [音频焦点增强功能](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#media-af)
    
        * [媒体指标](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#mm)
    
        * [MediaPlayer](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#mp)
    
        * [音频录制器](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#mr)
    
        * [音频播放控制](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#apc)
    
        * [增强的媒体文件访问功能](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#imfa)

    * [连接](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#cs)

        * [WLAN 感知](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#aware)
    
        * [蓝牙](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#bt)
    
        * [配套设备配对](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#cdp)

    * [共享](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#sh)

        * [智能共享](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#smsh)
    
        * [智能文本选择](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#sts)

    * [无障碍功能](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#a11y)

        * [无障碍功能按钮](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#ab)
    
        * [独立的音量调整](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#iva)
    
        * [指纹手势](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#fg)
    
        * [字词级突出显示](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#wlh)
    
        * [标准化单端范围值](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#sosrv)
    
        * [提示文本](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#ht)
    
        * [连续的手势分派](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#cgd)

    * [安全性与隐私](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#sp)

        * [权限](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#perms)
    
        * [新的帐号访问和 Discovery API](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#naa)
    
        * [Google Safe Browsing API](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#sb)

    * [测试](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#test)

        * [仪器测试](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#instr)
    
        * [用于测试的模拟 Intent](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#mit)

    * [运行时和工具](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#rt)

        * [平台优化](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#art)
    
        * [更新的 Java 支持](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#java)
    
        * [更新的 ICU4J Android Framework API](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#icu4j)
    
        * [Android 企业版](https://developer.android.google.cn/about/versions/oreo/android-8.0?hl=zh-cn#ae)

* [Android 8.1 新特性](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn)

    * [Android Oreo（Go 版本）](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn#go)

    * [Neural Networks API](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn#nnapi)

    * [自动填充框架更新](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn#autofill)

    * [通知](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn#notify)

    * [EditText 更新](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn#edittext)

    * [程序化安全浏览操作](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn#safebrowsing)

    * [视频缩略图提取器](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn#video-thumbnail)

    * [Shared memory API](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn#sharedmemory)

    * [WallpaperColors API](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn#wallpaper)

    * [指纹更新](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn#fingerprint)

    * [加密更新](https://developer.android.google.cn/about/versions/oreo/android-8.1?hl=zh-cn#crypto)

#### 行为变更

* [针对所有应用的行为变更](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#atap)

    * [后台执行限制](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#back-all)
    
    * [Android 后台位置限制](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#abll)
    
    * [应用快捷键](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#as)
    
    * [语言区域和国际化](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#lai)
    
    * [提醒窗口](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#all-aw)
    
    * [输入和导航](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#ian)
    
    * [网页表单自动填充](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#wfa)
    
    * [无障碍功能](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#a11y)
    
    * [网络连接和 HTTP(S) 连接](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#networking-all)
    
    * [蓝牙](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#bt)
    
    * [无缝连接](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#sc)
    
    * [安全性](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#security-all)
    
    * [隐私性](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#privacy-all)
    
    * [记录未捕获的异常](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#loue)
    
    * [联系人提供程序使用情况统计方法的变更](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#cpu)
    
    * [集合的处理](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#ch-all)
    
    * [Android 企业版](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#work)

* [针对 targetSdkVersion 26+ 应用的行为变更](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#o-apps)

    * [提醒窗口](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#cwt)
    
    * [内容变更通知](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#ccn)
    
    * [视图焦点](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#o-vf)
    
    * [安全性](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#o-sec)
    
    * [帐号访问和可检测性](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#aaad)
    
    * [隐私性](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#o-pri)
    
    * [权限](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#rmp)
    
    * [媒体](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#med)
    
    * [原生库](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#nl)
    
    * [集合的处理](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#o-ch)
    
    * [类加载行为](https://developer.android.google.cn/about/versions/oreo/android-8.0-changes?hl=zh-cn#o-cl)

#### 相关资源

* 适配简介

    * [Android 8.0 适配指北](https://weilu.blog.csdn.net/article/details/80965631)

* 厂商适配指南

    * [VIVO 开放平台 - Android 8.0 适配指南](https://dev.vivo.com.cn/documentCenter/doc/105)

* 通知渠道适配

    * [Android 通知栏微技巧，8.0 系统中通知栏的适配](https://blog.csdn.net/guolin_blog/article/details/79854070)

    * [创建和管理通知渠道](https://developer.android.google.cn/training/notify-user/channels)

    * [Android 应用图标微技巧，8.0 系统中应用图标的适配](https://blog.csdn.net/guolin_blog/article/details/79417483)

* 透明 Activity 方向适配

    * [Android 8.0 踩坑记录 - Only fullscreen opaque activities can request orientation](https://www.jianshu.com/p/d0d907754603)

    * [Only fullscreen opaque activities can request orientation 问题及解决方案](https://www.jianshu.com/p/fbfec24d7916)

    * [Only fullscreen activities can request orientation 终极解决方法](https://blog.csdn.net/starry_eve/article/details/82777160)

    * ["Only fullscreen opaque activities can request orientation "问题再分析](https://juejin.cn/post/6844903808485556232)

* 启动后台 Service 适配

    * [Android 8.0 启动后台service 出错 IllegalStateException: Not allowed to start service Intent](https://blog.csdn.net/u010784887/article/details/79675147)

    * [Android 8.0 + Service开启方式兼容处理](https://blog.csdn.net/o279642707/article/details/82352431)

    * [Context.startForegroundService() did not then call Service.startForeground？](https://blog.csdn.net/sinat_20059415/article/details/80584487)

    * [Android 8.0: java.lang.IllegalStateException: Not allowed to start service Intent](https://stackoverflow.com/questions/46445265/android-8-0-java-lang-illegalstateexception-not-allowed-to-start-service-inten)

* 画中画适配

    * [Android画中画（PIP）全解析，踩坑记录](https://juejin.cn/post/7301544527478685731)

    * [Android 原生 Picture in Picture 画中画功能避坑指南](https://juejin.cn/post/7240444181326807101)

    * [Android -- 系统画中画实践指南](https://juejin.cn/post/7276696116905394228)

    * [如何在 Android 中实现画中画功能](https://mp.weixin.qq.com/s/oC4qJudTd99dfyk2wwt2ZQ)

* 其他适配

    * [适配 Anddroid 8.0 多语言的解决方案](https://github.com/getActivity/MultiLanguages)

## Android 7.0 / 7.1.1

#### 新特性

* [Android 7.0 新特性](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn)

    * [多窗口支持](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#multi-window_support)

    * [通知增强功能](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#notification_enhancements)

    * [配置文件指导的 JIT/AOT 编译](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#jit_aot)

    * [快速的应用安装路径](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#quick_path_to_app_install)

    * [随时随地低电耗模式](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#doze_on_the_go)

    * [后台优化](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#background_optimizations)

    * [SurfaceView](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#surfaceview)

    * [流量节省程序](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#data_saver)

    * [Vulkan API](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#vulkan)

    * [Quick Settings Tile API](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#tile_api)

    * [号码屏蔽](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#number-blocking)

    * [来电过滤](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#call_screening)

    * [多语言区域支持，更多语言](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#multi-locale_languages)

    * [新增的表情符号](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#emoji)

    * [Android 中的 ICU4J API](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#icu4)

    * [WebView](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#webview)

        * [Chrome 和 WebView 配合使用](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#chrome-%E5%92%8C-webview-%E9%85%8D%E5%90%88%E4%BD%BF%E7%94%A8)

        * [多进程](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#%E5%A4%9A%E8%BF%9B%E7%A8%8B)

        * [Javascript 在页面加载之前运行](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#javascript-%E5%9C%A8%E9%A1%B5%E9%9D%A2%E5%8A%A0%E8%BD%BD%E4%B9%8B%E5%89%8D%E8%BF%90%E8%A1%8C)

        * [不安全起点上的地理定位](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#%E4%B8%8D%E5%AE%89%E5%85%A8%E8%B5%B7%E7%82%B9%E4%B8%8A%E7%9A%84%E5%9C%B0%E7%90%86%E5%AE%9A%E4%BD%8D)

        * [测试 WebView 测试版](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#%E6%B5%8B%E8%AF%95-webview-%E6%B5%8B%E8%AF%95%E7%89%88)

    * [OpenGL™ ES 3.2 API](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#gles_32)

    * [Android TV 录制](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#android_tv_recording)

    * [Android for Work](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#android_for_work)

        * [工作资料安全性挑战](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#work_profile_security_challenge)
    
        * [关闭工作](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#turn_off_work)
    
        * [Always on VPN](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#always_on_vpn)
    
        * [自定义配置](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#custom_provisioning)

    * [无障碍增强功能](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#accessibility_enhancements)

    * [直接启动](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#direct_boot)

    * [密钥认证](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#key_attestation)

    * [网络安全性配置](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#network_security_config)

    * [默认受信任的证书颁发机构](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#default_trusted_ca)

    * [APK signature scheme v2](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#apk_signature_v2)

    * [作用域目录访问](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#scoped_directory_access)

    * [键盘快捷键辅助工具](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#keyboard_shortcuts_helper)

    * [Custom Pointer API](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#custom_pointer_api)

    * [Sustained Performance API](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#sustained_performance_api)

    * [VR 支持](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#vr)

    * [打印服务增强](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#print_svc)

    * [FrameMetricsListener API](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#framemetrics_api)

    * [虚拟文件](https://developer.android.google.cn/about/versions/nougat/android-7.0?hl=zh-cn#virtual_files)

* [Android 7.1 新特性](https://developer.android.google.cn/about/versions/nougat/android-7.1?hl=zh-cn)

    * [应用快捷方式](https://developer.android.google.cn/about/versions/nougat/android-7.1?hl=zh-cn#shortcuts)

    * [键盘支持图像](https://developer.android.google.cn/about/versions/nougat/android-7.1?hl=zh-cn#img-kbd)

    * [新的专业表情符号](https://developer.android.google.cn/about/versions/nougat/android-7.1?hl=zh-cn#new-emoji)

    * [增强的动态壁纸元数据](https://developer.android.google.cn/about/versions/nougat/android-7.1?hl=zh-cn#live-wp-metadata)

    * [圆形图标资源](https://developer.android.google.cn/about/versions/nougat/android-7.1?hl=zh-cn#circular-icons)

    * [存储管理器意图](https://developer.android.google.cn/about/versions/nougat/android-7.1?hl=zh-cn#storage-mgr-intent)

    * [改进的 VR 线程调度](https://developer.android.google.cn/about/versions/nougat/android-7.1?hl=zh-cn#vr-scheduling)

    * [演示用户提示](https://developer.android.google.cn/about/versions/nougat/android-7.1?hl=zh-cn#demo-hint)

    * [运营商和呼叫应用程序的 API](https://developer.android.google.cn/about/versions/nougat/android-7.1?hl=zh-cn#carrier-apis)

    * [可穿戴设备的新屏幕密度](https://developer.android.google.cn/about/versions/nougat/android-7.1?hl=zh-cn#wear-screen)

#### 行为变更

* [电池和内存](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#perf)

    * [低电耗模式](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#doze)

    * [后台优化](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#bg-opt)

* [系统权限更改](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#permfilesys)

* [在应用间共享文件](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#sharing-files)

* [无障碍改进](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#accessibility)

    * [屏幕缩放](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#screen-zoom)

    * [设置向导中的视觉设置](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#vision-settings)

* [NDK 应用链接至平台库](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#ndk)

    * [检查您的应用是否使用私有库](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#ndk-errors)

    * [更新您的应用](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#ndk-update)

* [Android for Work](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#afw)

* [注解保留](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#annotations)

* [其他重要说明](https://developer.android.google.cn/about/versions/nougat/android-7.0-changes?hl=zh-cn#other)

#### 相关资源

* 适配简介

    * [Android 7.0 脱坑指南](https://weilu.blog.csdn.net/article/details/77404712)

    * [Android 7.0 适配教程，心得](https://www.jianshu.com/p/56b9fb319310)

* FileProvider适配

    * [Android 一起来看看 7.0 的新特性 FileProvider](https://www.jianshu.com/p/be817f3aa145)

    * [官方文档 - FileProvider 类](https://developer.android.google.cn/reference/androidx/core/content/FileProvider?hl=zh-cn)

* 其他适配

    * [Toast 在 Android 7.1 崩溃排查及修复](https://www.jianshu.com/p/437f473017d6)

    * [PopupWindow 在 Android N(7.0) 的兼容性问题](https://www.jianshu.com/p/0df10893bf5b)

    * [Android 7.0 WebView 部分机型打不开](https://blog.csdn.net/u012347067/article/details/70829013)

## Android 6.0

#### 新特性

* [指纹身份验证](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#fingerprint-authentication)

* [确认凭据](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#confirm-credential)

* [应用链接](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#app-linking)

* [自动备份应用](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#backup)

* [直接共享](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#direct-share)

* [语音交互](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#voice-interactions)

* [Assist API](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#assist)

* [可采用的存储设备](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#adoptable-storage)

* [通知](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#notifications)

* [蓝牙触控笔支持](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#bluetooth-stylus)

* [改进的蓝牙低功耗扫描](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#ble-scanning)

* [Hotspot 2.0 第 1 版支持](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#hotspot)

* [4K 显示模式](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#4K-display)

* [主题化 ColorStateList](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#behavior-themeable-colorstatelists)

* [音频功能](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#audio)

* [视频功能](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#video)

* [相机功能](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#camera)

    * [Flashlight API](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#flashlight)

    * [Reprocessing API](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#reprocessing)

* [Android for Work 功能](https://developer.android.google.cn/about/versions/marshmallow/android-6.0?hl=zh-cn#afw)

#### 行为变更

* [运行时权限](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-runtime-permissions)

* [低电耗模式和应用待机模式](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-power)

* [取消支持 Apache HTTP 客户端](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-apache-http-client)

* [BoringSSL](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#boringSSL)

* [硬件标识符访问权](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-hardware-id)

* [通知](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-notifications)

* [音频管理器变更](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-audiomanager-Changes)

* [文本选择](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-text-selection)

* [浏览器书签变更](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-bookmark-browser)

* [Android 密钥库变更](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-keystore)

* [WLAN 和网络连接变更](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-network)

* [相机服务变更](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-camera)

* [运行时](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-runtime)

* [APK 验证](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-apk-validation)

* [USB 连接](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-usb)

* [Android for Work 变更](https://developer.android.google.cn/about/versions/marshmallow/android-6.0-changes?hl=zh-cn#behavior-afw)

#### 相关资源

* [Android 6.0 运行权限解析](https://www.jianshu.com/p/6a4dff744031)

* [官方文档 - 请求应用权限](https://developer.android.google.cn/training/permissions/requesting.html)

* [所有的 Android 权限清单](https://developer.android.google.cn/reference/android/Manifest.permission?hl=zh_cn)

* [Android M 的 NDK 行为变更对 APK 包体积的影响](https://www.sunzn.com/2020/06/05/Android-M-%E7%9A%84-NDK-%E8%A1%8C%E4%B8%BA%E5%8F%98%E6%9B%B4%E5%AF%B9-APK-%E5%8C%85%E4%BD%93%E7%A7%AF%E7%9A%84%E5%BD%B1%E5%93%8D/)

## Android 5.0 / 5.1

#### 新特性

* [Android 5.0 新特性](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn)

    * [用户界面](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#UI)

        * [Material Design 支持](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#MaterialDesign)

        * [最近使用的应用屏幕中的并发文档和 Activity](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Recents)

        * [WebView 更新](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#WebView)

        * [屏幕采集和共享](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#ScreenCapture)

    * [通知](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Notifications    )

        * [锁定屏幕通知](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#LockscreenNotifications)

        * [通知元数据](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#NotificationsMetadata)

    * [图形](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Graphics)

        * [对 OpenGL ES 3.1 的支持](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#OpenGLES-3-1)

        * [Android 扩展包](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#AndroidExtensionPack)

    * [媒体](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Media)

        * [用于高级相机功能的 Camera API](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Camera-v2)

        * [音频回放](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#AudioPlayback)

        * [媒体回放控制](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#MediaPlaybackControl)

        * [媒体浏览](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#MediaBrowsing)

    * [存储](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Storage)

        * [目录选择](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#DirectorySelection)

    * [无线和连接](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Wireless)

        * [多个网络连接](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Multinetwork)

        * [蓝牙低功耗](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#BluetoothBroadcasting)

        * [NFC 增强功能](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#NFCEnhancements)

    * [Volta 项目](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Power)

        * [计划排定作业](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#JobScheduler)

        * [电池使用开发者工具](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#PowerMeasurementTools)

    * [工作场所和教育领域中的 Android](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Enterprise)

        * [托管配置](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#ManagedProvisioning)

        * [设备所有者](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#DeviceOwner)

        * [固定屏幕](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#ScreenPinning)

    * [打印框架](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Printing)

        * [将 PDF 渲染成位图](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#PDFRender)

    * [系统](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#System)

        * [应用使用情况统计信息](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#AppUsageStatistics)

    * [测试与辅助工具](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#TestingA11y)

    * [测试与辅助工具改进](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#TestingA11yImprovements)

    * [IME](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#IME)

        * [更方便的输入语言切换](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Switching)

    * [清单声明](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Manifest)

        * [可声明的必备功能](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#ManifestFeatures)

        * [用户权限](https://developer.android.google.cn/about/versions/android-5.0?hl=zh-cn#Permissions)

* [Android 5.1 新特性](https://developer.android.google.cn/about/versions/android-5.1?hl=zh-cn)

    * [多 SIM 卡支持](https://developer.android.google.cn/about/versions/android-5.1?hl=zh-cn#multisim)

    * [已弃用的 HTTP 类](https://developer.android.google.cn/about/versions/android-5.1?hl=zh-cn#http)

    * [运营商服务](https://developer.android.google.cn/about/versions/android-5.1?hl=zh-cn#carrier)

#### 行为变更

* [Android Runtime (ART)](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#ART)

* [通知](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#BehaviorNotifications)

    * [Material Design 样式](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#NotificationsMaterialDesignStyle)

    * [声音和振动](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#NotificationsSoundVibration)

    * [锁定屏幕可见性](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#NotificationsLockscreenVisibility)

    * [媒体播放](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#NotificationsMediaPlayback)

    * [浮动通知](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#NotificationsHeadsup)

* [媒体控件和 RemoteControlClient](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#BehaviorMediaControl)

* [getRecentTasks()](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#BehaviorGetRecentTasks)

* [Android NDK 中的 64 位支持](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#64BitSupport)

* [绑定到服务](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#BindService)

* [WebView](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#BehaviorWebView)

* [自定义权限唯一性要求](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#custom_permissions)

    * [使用重复的自定义权限的应用](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#%E4%BD%BF%E7%94%A8%E9%87%8D%E5%A4%8D%E7%9A%84%E8%87%AA%E5%AE%9A%E4%B9%89%E6%9D%83%E9%99%90%E7%9A%84%E5%BA%94%E7%94%A8)

    * [您的应用需要注意的事项](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#%E6%82%A8%E7%9A%84%E5%BA%94%E7%94%A8%E9%9C%80%E8%A6%81%E6%B3%A8%E6%84%8F%E7%9A%84%E4%BA%8B%E9%A1%B9)

    * [新安装和更新](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#%E6%96%B0%E5%AE%89%E8%A3%85%E5%92%8C%E6%9B%B4%E6%96%B0)

    * [使用 Android 5.0 系统更新的现有安装](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#%E4%BD%BF%E7%94%A8-android-5.0-%E7%B3%BB%E7%BB%9F%E6%9B%B4%E6%96%B0%E7%9A%84%E7%8E%B0%E6%9C%89%E5%AE%89%E8%A3%85)

    * [建议](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#%E5%BB%BA%E8%AE%AE)

* [TLS/SSL 默认配置变更](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#ssl)

    * [服务器不支持任何已启用的加密套件](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8D%E6%94%AF%E6%8C%81%E4%BB%BB%E4%BD%95%E5%B7%B2%E5%90%AF%E7%94%A8%E7%9A%84%E5%8A%A0%E5%AF%86%E5%A5%97%E4%BB%B6)

    * [应用对用于连接服务器的加密套件做出错误的假设](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#%E5%BA%94%E7%94%A8%E5%AF%B9%E7%94%A8%E4%BA%8E%E8%BF%9E%E6%8E%A5%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E5%8A%A0%E5%AF%86%E5%A5%97%E4%BB%B6%E5%81%9A%E5%87%BA%E9%94%99%E8%AF%AF%E7%9A%84%E5%81%87%E8%AE%BE)

    * [服务器不支持 TLSv1.1、TLSv1.2 或新的 TLS 扩展](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8D%E6%94%AF%E6%8C%81-tlsv1.1%E3%80%81tlsv1.2-%E6%88%96%E6%96%B0%E7%9A%84-tls-%E6%89%A9%E5%B1%95)

* [支持托管配置文件](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#managed_profiles)

    * [处理 Intent](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#mg_profile_intents)

    * [在各个配置文件中共享文件](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#mp_profile_file_sharing)

    * [已移除锁定屏幕小部件支持](https://developer.android.google.cn/about/versions/android-5.0-changes?hl=zh-cn#%E5%B7%B2%E7%A7%BB%E9%99%A4%E9%94%81%E5%AE%9A%E5%B1%8F%E5%B9%95%E5%B0%8F%E9%83%A8%E4%BB%B6%E6%94%AF%E6%8C%81)

## Android 4.4

#### 新特性

* [打印框架](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#Printing)

    * [打印通用内容](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#PrintingGeneric)

    * [打印图像](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#PrintingImages)

    * [构建打印服务](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#PrintService)

* [短信提供程序](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#SMS)

* [无线和连接](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#Wireless)

    * [主机卡模拟](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#HCE)

    * [NFC 读取器模式](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#ReaderMode)

    * [红外线发射器](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#IR)

* [多媒体](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#Multimedia)

    * [自适应播放](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#AdaptivePlayback)

    * [音频点播时间戳](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#AudioTimestamp)

    * [Surface 图像读取器](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#ImageReader)

    * [峰值和有效值 (RMS) 测量](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#PeakRms)

    * [音量增强器](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#LoudnessEnhancer)

    * [遥控器](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#RemoteController)

    * [从遥控器进行评分](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#Ratings)

    * [隐藏式字幕](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#ClosedCaptions)

* [动画和图形](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#Animations)

    * [场景和转场](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#Transitions)

    * [动画暂停](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#AnimatorPause)

    * [可重复使用的位图](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#ReusableBitmaps)

* [用户内容](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#UserContent)

    * [存储访问框架](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#StorageAccess)

    * [外部存储空间访问](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#ExternalStorage)

    * [同步适配器](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#SyncAdapter)

* [用户输入](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#UserInput)

    * [新传感器类型](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#NewSensors)

    * [批处理传感器事件](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#BatchSensors)

    * [控制器身份](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#Controllers)

* [用户界面](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#UI)

    * [沉浸式全屏模式](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#ImmersiveMode)

    * [透明系统状态栏](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#TranslucentBars)

    * [增强的通知侦听器](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#NotificationListener)

    * [可绘制的 RTL 布局镜像](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#DrawableMirroring)

    * [无障碍功能](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#A11y)

* [应用权限](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#Permissions)

* [设备功能](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#DeviceFeatures)

#### 行为变更

* [外部存储](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#BehaviorStorage)

* [WebView](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#BehaviorWebView)

* [AlarmManager](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#BehaviorAlarms)

* [ContentResolver](https://developer.android.google.cn/about/versions/android-4.4?hl=zh-cn#BehaviorSync)

#### 相关资源

* [Android通知还能这么玩？](https://juejin.cn/post/7046282271237603341)

* [Android NotificationListenerService 的使用](https://blog.csdn.net/HuaKaiBuXiangLi/article/details/79064363)

* [Android 通知使用权（NotificationListenerService）的使用](https://blog.csdn.net/lyz_zyx/article/details/65440927)

#### 作者其他开源项目

* 安卓技术中台：[AndroidProject](https://github.com/getActivity/AndroidProject) ![](https://img.shields.io/github/stars/getActivity/AndroidProject.svg) ![](https://img.shields.io/github/forks/getActivity/AndroidProject.svg)

* 安卓技术中台 Kt 版：[AndroidProject-Kotlin](https://github.com/getActivity/AndroidProject-Kotlin) ![](https://img.shields.io/github/stars/getActivity/AndroidProject-Kotlin.svg) ![](https://img.shields.io/github/forks/getActivity/AndroidProject-Kotlin.svg)

* 权限框架：[XXPermissions](https://github.com/getActivity/XXPermissions) ![](https://img.shields.io/github/stars/getActivity/XXPermissions.svg) ![](https://img.shields.io/github/forks/getActivity/XXPermissions.svg)

* 吐司框架：[Toaster](https://github.com/getActivity/Toaster) ![](https://img.shields.io/github/stars/getActivity/Toaster.svg) ![](https://img.shields.io/github/forks/getActivity/Toaster.svg)

* 网络框架：[EasyHttp](https://github.com/getActivity/EasyHttp) ![](https://img.shields.io/github/stars/getActivity/EasyHttp.svg) ![](https://img.shields.io/github/forks/getActivity/EasyHttp.svg)

* 标题栏框架：[TitleBar](https://github.com/getActivity/TitleBar) ![](https://img.shields.io/github/stars/getActivity/TitleBar.svg) ![](https://img.shields.io/github/forks/getActivity/TitleBar.svg)

* 悬浮窗框架：[EasyWindow](https://github.com/getActivity/EasyWindow) ![](https://img.shields.io/github/stars/getActivity/EasyWindow.svg) ![](https://img.shields.io/github/forks/getActivity/EasyWindow.svg)

* ShapeView 框架：[ShapeView](https://github.com/getActivity/ShapeView) ![](https://img.shields.io/github/stars/getActivity/ShapeView.svg) ![](https://img.shields.io/github/forks/getActivity/ShapeView.svg)

* ShapeDrawable 框架：[ShapeDrawable](https://github.com/getActivity/ShapeDrawable) ![](https://img.shields.io/github/stars/getActivity/ShapeDrawable.svg) ![](https://img.shields.io/github/forks/getActivity/ShapeDrawable.svg)

* 语种切换框架：[MultiLanguages](https://github.com/getActivity/MultiLanguages) ![](https://img.shields.io/github/stars/getActivity/MultiLanguages.svg) ![](https://img.shields.io/github/forks/getActivity/MultiLanguages.svg)

* Gson 解析容错：[GsonFactory](https://github.com/getActivity/GsonFactory) ![](https://img.shields.io/github/stars/getActivity/GsonFactory.svg) ![](https://img.shields.io/github/forks/getActivity/GsonFactory.svg)

* 日志查看框架：[Logcat](https://github.com/getActivity/Logcat) ![](https://img.shields.io/github/stars/getActivity/Logcat.svg) ![](https://img.shields.io/github/forks/getActivity/Logcat.svg)

* 嵌套滚动布局框架：[NestedScrollLayout](https://github.com/getActivity/NestedScrollLayout) ![](https://img.shields.io/github/stars/getActivity/NestedScrollLayout.svg) ![](https://img.shields.io/github/forks/getActivity/NestedScrollLayout.svg)

* Android 代码规范：[AndroidCodeStandard](https://github.com/getActivity/AndroidCodeStandard) ![](https://img.shields.io/github/stars/getActivity/AndroidCodeStandard.svg) ![](https://img.shields.io/github/forks/getActivity/AndroidCodeStandard.svg)

* Android 资源大汇总：[AndroidIndex](https://github.com/getActivity/AndroidIndex) ![](https://img.shields.io/github/stars/getActivity/AndroidIndex.svg) ![](https://img.shields.io/github/forks/getActivity/AndroidIndex.svg)

* Android 开源排行榜：[AndroidGithubBoss](https://github.com/getActivity/AndroidGithubBoss) ![](https://img.shields.io/github/stars/getActivity/AndroidGithubBoss.svg) ![](https://img.shields.io/github/forks/getActivity/AndroidGithubBoss.svg)

* Studio 精品插件：[StudioPlugins](https://github.com/getActivity/StudioPlugins) ![](https://img.shields.io/github/stars/getActivity/StudioPlugins.svg) ![](https://img.shields.io/github/forks/getActivity/StudioPlugins.svg)

* 表情包大集合：[EmojiPackage](https://github.com/getActivity/EmojiPackage) ![](https://img.shields.io/github/stars/getActivity/EmojiPackage.svg) ![](https://img.shields.io/github/forks/getActivity/EmojiPackage.svg)

* AI 资源大汇总：[AiIndex](https://github.com/getActivity/AiIndex) ![](https://img.shields.io/github/stars/getActivity/AiIndex.svg) ![](https://img.shields.io/github/forks/getActivity/AiIndex.svg)

* 省市区 Json 数据：[ProvinceJson](https://github.com/getActivity/ProvinceJson) ![](https://img.shields.io/github/stars/getActivity/ProvinceJson.svg) ![](https://img.shields.io/github/forks/getActivity/ProvinceJson.svg)

* Markdown 语法文档：[MarkdownDoc](https://github.com/getActivity/MarkdownDoc) ![](https://img.shields.io/github/stars/getActivity/MarkdownDoc.svg) ![](https://img.shields.io/github/forks/getActivity/MarkdownDoc.svg)

#### 微信公众号：Android轮子哥

![](https://raw.githubusercontent.com/getActivity/Donate/master/picture/official_ccount.png)

#### Android 技术 Q 群：10047167

#### 如果您觉得我的开源库帮你节省了大量的开发时间，请扫描下方的二维码随意打赏，要是能打赏个 10.24 :monkey_face:就太:thumbsup:了。您的支持将鼓励我继续创作:octocat:

![](https://raw.githubusercontent.com/getActivity/Donate/master/picture/pay_ali.png) ![](https://raw.githubusercontent.com/getActivity/Donate/master/picture/pay_wechat.png)

#### [点击查看捐赠列表](https://github.com/getActivity/Donate)

## License

```text
Copyright 2021 Huang JinQun

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```