# [iOS] UIScreen, UIWindow, UIView 比較

#### UIScreen

- 獲取實際螢幕的大小

```swift
UIScreen.mainScreen().bounds
UIScreen.mainScreen().applicationFrame
```

#### UIView

- 一矩形區域
- 負責管理其內的畫面、事件、互動，以及subView

#### UIWindow

- 特殊的UIView，所有View的root
- 一個App通常只有一個window，additional window多用於外部顯示器
- windows彼此獨立
- 有一個rootViewController property，管理其下所有事件與Views

自行建立有NavigationController 的 UIWindow（不靠storyboard）

```swift
let window = UIWindow(frame: UIScreen.mainScreen().bounds)
window.rootViewController = UINavigationController()
window.makeKeyAndVisible()
```
