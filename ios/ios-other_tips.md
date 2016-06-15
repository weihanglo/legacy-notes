# [iOS] Other tips

#### UIScrollView with Interface Builder

UIScrollView 在Interface  Builder中的autolayout行為和其他元件很不同，其內的subView需至少**給定height或width**(作為content size)，且需給定**subviews與scroll view的距離**。

#### autoresizing mask

bitwise computing 的 enum 似乎改成用array表示這樣，不再用 `|` 了 ,

```swift
let view = UIView()
view.autoresizingMask = [.FlexibleWidth, .FlexibleHeight]
```

#### device rotate animation

iOS 8 之後整為同一支API

```swift
override func viewWillTransitionToSize(size: CGSize, withTransitionCoordinator
coordinator: UIViewControllerTransitionCoordinator) {

    // will rotate

    coordinator.animateAlongsideTransition({ (context) in

    // rotate with animation

    }, completion: {(content) in

    // did rotate

    })
    super.viewWillTransitionToSize(size, withTransitionCoordinator: coordinator)
}
```
