# [iOS] View Controller Transition Delegate

#### 1. Delegation

在每一次present新的view controller時，如果有接`trasitioningDelegate`，
UIKit會呼叫`animationControllerForPresentedController(_:presentingController:sourceController:)`，來詢問它的**delegate**是否有客製化轉場，該方法的return object 就是掌管整個轉場的 **animator**

> 若return nil，才會呼叫系統built-in的轉場

同樣的，當要dismiss view controller 時，`animationControllerForDismissedController(_:)`被呼叫，此方法也需回傳一個  **animator object**

#### 2. Animator object

animator object 分為interactive與否兩種（在此不討論 第三種 presentation controller）

animator 需實作 `UIViewControllerAnimatedTransitioning` protocol

若是 interactive 則需實作 `UIViewControllerInteractiveTransitioning` protocol

#### 3. Animate transition in Animator

UIKit會詢問**animator**的`animateTransition()`方法，這個方法可以透過`transition context`上下文取得當前的 view controller 以及 要present的 view controller。

**animator** 還需實作 `transitionDuration(transitionContext: UIViewControllerContextTransitioning?) -> NSTimeInterval` 以提供transition所需的時間。

UIKit 會等待 **animator** 調用 `completeTransition(_:)` 方法告知轉場結束，才讓 presenting 進入 completion handler 的 closure，以及 **animator** 自己的 `animationEnded(_:)`的方法。
