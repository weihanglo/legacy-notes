# [iOS] 有關 View Controller

#### View Controller 架構圖

<img src="https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Art/VCPG_ControllerHierarchy_fig_1-1_2x.png" style="width: 400px">

#### View Controller 有兩種
- content: 顯示內容的 View Controller
- container: 管理儲存 child view controller的容器，有：
  + `UITabBarController`: 以array方式儲存
  + `UINavigationController`: 以stack方式儲存
  + `UISplitViewController`: 分割視窗，有master和detailViewController
  + `UIPageViewController`: 儲存多個childVC，常用來實作App導引教學


#### Some design tips
1. 善用系統提供的framework，例如：
  - UIKit
  - GameKit
  - Social
  - AVFoundation...

2. view controllers 之間保持獨立，利用protocol來溝通

#### Views life cycle

View Controller 狀態轉換圖
<img src="https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/Art/UIViewController%20Class%20Reference_2x.png" style="width: 400px">

<img src="http://cg2010studio.files.wordpress.com/2013/05/uiviewcontroller-lifecycle.jpg" style="width: 400px">

1. `init(coder:)`/`init(nibName:bundle:)`
2. `loadView()`
3. `viewDidLoad()` <-- 跑這支後，outlet才會連結到view controller
4. `viewWillAppear(_:)`
  - --> `viewWillLayoutSubviews()` (if need layout subviews)
  - --> `viewDidLayoutSubviews()`  (if need layout subviews)
5. `viewDidAppear(_:)`
6. `viewWillDisappear(_:)`
7. `viewDidDisappear(_:)`
8. `viewWillUnload()`
9. `viewDidUnload()`
10. `deinit()`

<img src="http://img.blog.csdn.net/20130621105945796?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveHl6X2xtbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" style="width: 400px">

#### Load view 的三種方法
- 這裡的 view 指的是 view controller 的 main view
- 透過 storyboard

```swift
let sb = UIStoryboard(name: "aStoryboard", bundle: nil)
let myVC = sb.instantiateInitialViewController()
// or a specified view controller
let myVC = sb.instantiateViewControllerWithIdentifier("myVC")
```

- 透過 xib/nib

```swift
let myVC = UIViewController(nibName: "aXibname", bundle: nil)
```

- 透過 loadView() method
- as Apple Document says, "You should not call these methods yourself."

```swift
override func loadView() {
    self.view = UIView()
}
```

#### memory warning flow chart
<img src="http://img.blog.csdn.net/20141213112711915?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzIzODc2OA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" style="width: 400px">
