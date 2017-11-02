---
title: View Controller 事件發生順序
categories:
- Swift 4.0
tags:
- Swift
---

在宣告或是配置ViewController中的元件時大多都會將View的初始化動作大多會放在viewDidLoad中配置， 但除了viewDidLoad 外其實還有其他的事件可以利用。

## Event使用的順序

### viewDidLoad:只會被呼叫一次
View 被載入時
``` bash

    override func viewDidLoad() {
        super.viewDidLoad()
        NSLog(@"viewDidLoad");
    }

``` 


### viewWillAppear
View 要被呈現前，發生於 viewDidLoad 之後:常常會被呼叫
``` bash

    override func viewWillAppear(_ animated: Bool) {        
        NSLog(@"viewWillAppear");
    }

``` 

### viewDidAppear
View 呈現後，發生於 viewWillAppear 之後
``` bash

    override func viewDidAppear(_ animated: Bool) {  
        NSLog(@"viewDidAppear");
    }

``` 


### viewDidDisappear
View 完全結束後，發生於 viewWillDisappear 之後
``` bash 

    override func viewDidDisappear(_ animated: Bool) {  
        NSLog(@"viewDidDisappear");
    }

``` 

為何在View載入時，要分成這麼多個部分進行動作呢？
因為，viewDidLoad是當第一次view載入，也就是說僅有第一次開啓時，才會動作，而viewWillAppear則是此controller欲顯示畫面的時候就會呼叫。

## viewController生命週期圖

[![](https://image.slidesharecdn.com/iosappdevelopment-140627191613-phpapp02/95/ios-app-storybard-app-iap-23-638.jpg)](viewController生命週期)



