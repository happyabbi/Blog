---
title: Grand Central Dispatch (GCD)
categories:
- Swift 4.0
tags:
- Swift
---

在多核心 CPU 或是雲端運算應用越來越普及的現在，平行多工處理變成十分重要和熱門的項目，近幾年 FP (Functional Programming) 越來越流行，相關程式語言越來越多可以看出這種趨向， Apple 在 snow leopard 和 iPhone OS 4.0 針對平行處理，多工等議題 加入了一個全新的功能 Grand Central Dispatch (GCD)，請參考 官方的說明頁面：

http://www.apple.com/tw/macosx/technology/

## 傳統多工處理的問題
傳統透過 thread 達成的多工不是十分容易寫，工程師必須處理大量 資料同步的問題，而且應用程式往往不容易取得真的系統資源資訊，如 目前同時有多少 thread 正在執行，系統可以處理的極限，當然很多 作業系統完全將這部份責任交給應用程式決定，基本上不會處理或是 透露太多 kernel 細節的部份，大不了就是效能不好，不然就是當機 無所謂。

## Asynchronous
Asynchronous，將一些需要比較多時間處理的問題交由背景執行以免造成 UI 或是其他程式停止執行， 造成使用者誤會當機或是不好的經驗。
Apple 在 Mac OS 10.6 和 iPhone OS 4.0 之後提供了名叫 Grand Central Dispatch (GCD) 的機制，將多工處理的 thread 統一由 OS 管理，以提供更好的效能。
工程師現在只要定義好 block 然後丟到符合需要的 dispatch queue 即可， dispatch queue 由系統直接維護，比起傳統的 thread 使用上會有些限制，不過更為安全也更簡單。
block可以把它想像成一種function即可。
Apple 另外提供 Operation Queues 的機制也可以實作平行處理或多工。
## Dispatch Queues

### Type：
* Serial
Serial Queue (private dispatch queues) 依照放入的順序一次執行一個 block，通常用於存取指定的資源。 我們可以依照需求建立許多不同的 Serial Queue
* Concurrent
Concurrent Queue (global dispatch queue) 依照放入的順序和系統目前 資源的狀態執行多個block。
* Main dispatch queue
在應用程式的main thread中執行被指定的動作。

### Creating Global Concurrent Dispatch Queue

``` swift
// 可依需要選擇 DISPATCH_QUEUE_PRIORITY_HIGH DISPATCH_QUEUE_PRIORITY_LOW
dispatch_queue_t aQueue =
  dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
```

### Creating Serial Dispatch Queues

由於Serial dispathc queue 一次只執行一個任務的特性，所以任務絕對會依照加入 的時間順序執行。

``` swift
dispatch_queue_t queue;
queue = dispatch_queue_create("com.example.MyQueue", NULL);
```
在 block 裡面可以取得目前 dispatch queue 的id: dispatch_get_current_queue(..)


### 執行 dispatch queue

``` swift
dispatch_queue_t queue = dispatch_queue_create("zenny_chen_firstQueue", NULL);
dispatch_async(queue, ^(void) {
     int sum = 0;
     for(int i = 0; i < 100; i++)
         sum += myArray[i];
     NSLog(@"The sum is: %d", sum);
     flag = YES;
 });
```

### Dispatch queue memory management

dispatch_retain() --> reference count +1 dispatch_release() --> reference count -1

dispatch_queue_creat() --> reference count = 1
reference count = 0 系統釋放 dispatch queue

### Callback function?

dispatch queue 要怎樣做到 callback 的機制，來得知工作已經完成，或是取得 運行的結果？

下面範例實作一種稱為 completion block 的機制，達到我們熟悉 callback 的 效果。

``` swift
// 第三四個參數就是用來作為 callback 的 queue 和 block
void average_async(int *data, size_t len,
     dispatch_queue_t queue, void (^completionBlock)(int))
{
     // 預防dispatch queue執行完成前queue被釋放。
     dispatch_retain(queue);

     dispatch_async( dispatch_get_global_queue( DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
         int avg = average(data,len);
         // 啟動一個dispatch queue 執行 completionBlock
         dispatch_async(queue, ^{completionBlock(avg);});
         dispatch_release(queue);
     });

}
```
這段程式先啟動 Concurrent dispatch queue 並在執行的 block 內計算平均值， 計算完畢後在啟動一個 Serial dispatch queue 呼叫函數參數傳入的callback block (completion block) 並傳回運算結果。



### 自定資料

dispatch object (queue, semaphore, group, source) 都可以隨我們開心 設定關連的額外資料，這資料可以是自己定義的 struct 或是 cocoa object 沒有 什麼特別的限制，唯一要注意的只有一點：

自行管理附帶資料的記憶體管理工作，如有需要請設定 queue 的 finalizer 做釋放 的工作。

``` swift
void myFinalizerFunction(void *context)
{
     MyDataContext* theData = (MyDataContext *)context;

     // Clean up the contents of the structure
     myCleanUpDataContextFunction(theData);

     // Now release the structure itself.
     free(theData);
}

dispatch_queue_t createMyQueue()
{
     MyDataContext*  data = (MyDataContext*) malloc(sizeof(MyDataContext));
     myInitializeDataContextFunction(data);

     // Create the queue and set the context data.
     dispatch_queue_t serialQueue = dispatch_queue_create("com.example.CriticalTaskQueue", NULL);
     if (serialQueue)
     {
         dispatch_set_context(serialQueue, data);
         dispatch_set_finalizer_f(serialQueue, &myFinalizerFunction);
     }

     return serialQueue;
}

```


### Semaphore

dispatch_semaphore_signal() --> semophore count +1 dispatch_semaphore_wait() --> semophore count -1

``` swift
__block dispatch_semaphore_t sem = dispatch_semaphore_create(0);

dispatch_queue_t queue = dispatch_queue_create("zenny_chen_firstQueue", nil);
dispatch_async(queue, ^(void) {
    int sum = 0;
    for(int i = 0; i < 100; i++)
        sum += myArray[i];
    NSLog(@"The sum is: %d", sum);

    // signal the semaphore
    dispatch_semaphore_signal(sem);
});

// wait for the semaphore
dispatch_semaphore_wait(sem, DISPATCH_TIME_FOREVER);

dispatch_release(queue);

```


### Loop Concurrently

如果你有一個工作要做很多次，然後他們的先後順序又不是那麼重要的時候， 可以使用 dispatch_apply() 或 dispatch_apply_f() 增加效率。

dispatch_apply() 依照給予的參數將 block 或是 function 排給 queue 執行，雖然他也可以在 Serial dispatch queue 裡面使用，但是由於 serial dispatch queue 一次只會做一件事對於增加程式效率其實沒什麼幫助。

``` swift
// 等效 code
for (i=0; i<count; i++)
{
    printf("%u\n",i);
}
// 提昇效能版本
dispatch_queue_t queue = dispatch_get_global_queue(
                 DISPATCH_QUEUE_PRIORITY_DEFAULT,0);
// i = 0 to 10
dispatch_apply(10, queue, ^(size_t i) {
    printf("%u\n",i);
});
```

### Suspending and Resuming Queues

suspending 不會停止目前正在處理的 block ，而是等到 block 結束後才停止。

dispatch_suspend()
dispatch_resume()


### Waiting on Group of Queue

Dispatch groups 提供更方便的等待機制，當我們必須等待一個或一個以上的 queue 處理玩工作時使用 dispatch group 可以省下不少事情。

``` swift
dispatch_queue_t queue=
    dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT,0);
dispatch_group_t group = dispatch_group_creat();

// Add task to the group
dispatch_group_async(group, queue, ^{
    // Some asynchronous work
});

// Do some other work while the tasks execute.

// wait on the group to block the current thread.
dispatch_group_wait(group, DISPATCH_TIME_FOREVER);
dispatch_release(group);
```



