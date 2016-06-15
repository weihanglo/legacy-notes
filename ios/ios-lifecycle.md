# [iOS] App 生命週期

五種 APP state
-------------

<img src="https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Art/high_level_flow_2x.png" style="width: 400px">

- Not running：app未運行
- Inactive：在foreground運行，未接收event
- Active：在foreground運行，正在接收event
- Background：在background運行，正在執行一些code
- Suspended：在background運行，未執行code。*可能在memory不夠時被終止*

#### 時機1：啟動App
State: Not running → Inactive
> 呼叫 `application(_:willFinishLaunchingWithOptions:)` 方法
> 發出 `UIApplicationDidFinishLaunchingNotification` 通知

State: Inactive → Active
> 呼叫 `applicationDidBecomeActive(_:)` 方法
> 發出 `UIApplicationDidBecomeActiveNotification`通知

#### 時機2：切換到其他App
State: Active → Inactive
> 呼叫 `applicationWillResignActive(_:) 方法
> 發出 `UIApplicationWillResignActiveNotification` 通知

State: Inactive → Background
> 呼叫 `applicationDidEnterBackground(_:)` 方法
> 發出 ` UIApplicationDidEnterBackgroundNotification` 通知


#### 時機3：切換至原本的App
State: Background → Inactive
> 呼叫 `applicationWillEnterForeground(_:) 方法
> 發出 `UIApplicationWillEnterForegroundNotification` 通知


State: Inactive → Active
> 呼叫 `applicationDidBecomeActive(_:)` 方法
> 發出 `UIApplicationDidBecomeActiveNotification`通知

#### 時機4：螢幕鎖定
同**切換App**

#### 時機5：關閉App
> 呼叫 `applicationWillTerminate(_:)` 方法
> 發出 `UIApplicationWillTerminateNotification` 通知

#### 官方圖說 [source](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/StrategiesforHandlingAppStateTransitions/StrategiesforHandlingAppStateTransitions.html)

- Foreground Launching
<img src="https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Art/app_launch_fg_2x.png" style="width: 400px">

- Background Launching
<img src="https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Art/app_launch_bg_2x.png" style="width: 400px">

- Interruptions
<img src="https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Art/app_interruptions_2x.png" style="width: 400px">

- Enter Foreground
<img src="https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Art/app_enter_foreground_2x.png" style="width: 400px">

- Background Life Cycle
<img src="https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Art/app_bg_life_cycle_2x.png" style="width: 400px">
