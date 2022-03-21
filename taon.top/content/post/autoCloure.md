---
title: "AutoCloure"
date: 2022-03-18T17:39:41+08:00
---

### @AutoCloure 用法记录
和原来理解的不同，有一种说法是，@AutoCloure主要的用途是延迟计算，当函数的参数需要延迟时，使用@AutoCloure可以达到目标。
```swift
import UIKit

var greeting = "Hello, playground"
func 🍉(){
    print("🍉")
    wow(bPrint:true,count:🆘() + 10)
}
func 🆘()->Int{
    print("help")
    return 9
}
var aa:Int?
let ssdsdf = 🆘()
let b =  aa ?? ssdsdf

func wow(bPrint:Bool, count:@autoclosure ()-> Int){
    if bPrint{
        print( count() )
    }
}
🍉()
```
上面代码中，🆘()方法是否调用，取决于wow函数中的逻辑，并不是作为函数参数一定会被调用。