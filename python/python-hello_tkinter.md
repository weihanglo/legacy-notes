# [Python] Tkinter 初探


## 1. Geometry Manager
Tk 有三種 geometry/layout manager: `pack`, `grid`, `place`。同一個master下的direct children widget，需使用同一種geometry manager。

#### 1. pack
將widget一個接著一個放置。實際上是在master下建立一個children widget list。

#### 2. grid
以grid的方式，指定row column來呈現children widget，一個cell管理一個widget。可以有rowspan、columnspan使widget佔用兩個以上的cell。

#### 3. place
直接指定坐標。

## 2. Useful Design Pattern
#### Target-Event Pattern
- binding event
- virtual event

#### Observer Pattern
須將Python的variable封裝成Tcl的variable，種類如下:

- BooleanVar
- DoubleVar
- IntVar
- StringVar

使用Variable的trace方法來實作Observer Pattern:

```python
from tkinter import *

def callback(*args):
    doSomething()

var = IntVar()
var.trace('w', callback)
```

var.trace的第一個參數是欲觀察mode，呼叫observer的時機如下:

- `r` read: variable被讀取時
- `w` write: variable被寫入時
- `u` undefine: variable轉為未定義時，也就是被delete

callback function傳入argument小技巧－－**使用lambda**

```python
value = 'would be passed to callback'
button = Button(root, text = value, command = lambda: callback(value))
```
