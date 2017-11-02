---
title: 如何理解 if let 與guard?
categories:
- Swift 4.0
tags:
- Swift
---
if let and guard只是省略的寫法，沒有也可以。但有了它們可以使得Code更為簡潔方便。所以要理解let和guard，不妨設想假如沒有這兩者，Code該怎麼寫。


## if let

``` bash
    func doSomething(str: String?)
    {
        let v: String! = str  
        if v != nil
        {
            // use v to do something
        }
    }
```
Swift 中因為有optional, 經常需要判斷是否為空。假如沒有if let，大致寫成上面的樣子，有了 if let, 可以改寫成

``` bash
    func doSomething(str: String?)
    {
        //if let，（可選綁定）上面等同於 v != nil
        if let v = str  
        {
            // use v to do something
        }
    }
```

上面兩段Code的寫法結果是一樣的。對照著，可以看出if let的寫法更加簡潔方便。


## guard

假如 if 中出現的Code很長，我們寫Code時可以將錯誤情況先返回。例如：
``` bash
func doSomething(str: String?)
{
    let v: String! = str
    if v == nil
    {
        return
    }
    // use v to do something
}
```

這樣做可以避免過多的嵌套。上面Code實在太常見了，swift也提供一個guard這個語法，用guard可以改寫成：

``` bash
func doSomething(str: String?)
{
    //guard： 用來處理提前返回，給str重新賦值，如果str=nil，直接return。優點是防止代碼嵌套過多。
    guard let v = str else { return }  
    // use v to do something
}
```
上面兩段的結果是一樣的。也可以看出guard的寫法更加簡潔方便。
