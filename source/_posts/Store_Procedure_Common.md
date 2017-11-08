---
title: Store Procedure - Common
categories:
- T-SQL
tags:
- SQL
---

## 判斷 temp table 是否存在
``` bash
    IF OBJECT_ID('tempdb..#MaintainUnitPrice') IS NOT NULL
      DROP TABLE #MaintainUnitPrice      
``` 
## 避免使用下面語法
``` bash
   DROP TABLE IF EXISTS #MaintainUnitPrice;      
```

## SP中使用同一DB的物件, 不要再加上 DB Name

## 判斷是否存在資料,請用以下寫法

``` bash
   IF EXISTS(SELECT 1 FROM [dbo].[Data_Header] WHERE [DATANo = @inDataNo])      
```
