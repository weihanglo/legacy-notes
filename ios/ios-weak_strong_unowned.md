# [iOS] Weak, Strong, Unowned 比較

#### ARC (Automatic Reference Counting)

Apple的自動記憶體管理技術，簡單來說就是：

> 在無任何 variable, constant 或 property 有**strong reference** 到該類別實例時（reference count == 0），該實例的記憶體空間就會被釋放。
> 一般情況下，variable，constant 或 property皆以 strong reference 到類別實例 (Swift)


#### Strong

就是一個pointer，會將 reference count +1，保護該object 不被ARC釋放。
在swift中用let 宣告的變數皆為 strong reference

#### Weak

- 宣告的變數需是一個可選值 Optional
- reference count 不會 +1
- 若只剩此 weak reference 到該instance，將立刻被釋放（和有GC的語言不一樣，不會留有cache）
- **swift** 中 weak reference 需以變數 **var** 宣告（因為需為Optional)

```swift
// this will failed to compile
weak let toCompiled = "failed"
```

#### Unowned

與weak相同，唯一的差異是uonwed非Optional，通常用於確定在使用unowned reference時，被referred 的物件不會變成nil

> unowned _對映到 objc 的_ `unsafe_unretained`


#### Swift 在 closure 中宣告 **capture list** 的 reference type

因 closure 本身和class一樣是 **reference types** 而非 **value types**，且有 capture 的特性，易產生 strong reference，需要設 `weak` 或 `unowned`，例如

```swift
{ [unowned self, weak delegate = self.delegate!] (parameter) -> Void in
    self.doSomething()
    variable.doAnotherThing()
}
```

兩句話說明 unowned V.S weak 在closure中的使用時機：

> If self could be nil in the closure use [weak self].
> If self will never be nil in the closure use [unowned self].

#### strongSelf 的用處

- 使用時機：當reference到的instance需要在 block的生命週期中被retain時。
- 使用實例： asynchronous downloading?
- 說明：self若被deunrefernce，strongSelf會繼續retain self 直到 block結束。若是weak reference，self很可能在afterDownload()之前被release。

```objective-c
__weak typeof(self) weakSelf = self

dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_BACKGROUND, 0), ^{
    __strong typeof(self) strongSelf = weakSelf
    if (strongSelf) {
        strongSelf.startDownload()
        strongSelf.afterDownload()
    }
})
```

```swift
dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_BACKGORUND, 0)){ [weak self] in
    if let strongSelf = self {
        storngSelf.startDownload()
        strongSelf.afterDownload()
    }
}
```


#### deinit/dealloc

在該 class instance 將從記憶體釋放時，會叫這一支method，可用來做一些釋放前的 finialize工作（例如remove notification）。

若存在retain cycle，reference count 無法歸零，則不會呼叫`deinit`/`dealloc`
