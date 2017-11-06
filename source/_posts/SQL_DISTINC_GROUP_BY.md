---
title: SQL DISTINCT / GROUP BY 
categories:
- SQl
tags:
- SQL basic
---

## DISTINCT

DISTINCT 只能指定一個欄位去除重複的值。如果有查詢出來有 A B C 三個欄位，想要 B 欄位值是獨一無二的，應該把 B 欄位放在最前面，在它前面加上 DISTINCT，例如：

``` sql
   SELECT DISTINCT B , A , C FROM TABLE
``` 

## GROUP BY
不同於 DISTINCT ， GROUP BY 會以多欄位的值作為一個群組，去除這個群組的重複值。所以查詢列出的欄位都必須加入 GROUP BY。例如：查詢出來有 A B C 三個欄位，GROUP BY 會以這三個欄位為一組，去除三個欄位共有的重複值。

``` sql
   SELECT B , A , C FROM TABLE GROUP BY A , B , C
``` 

## GROUP BY HAVING
在 GROUP BY 已經完成群組過濾作業之後， HAVING 才起作用，扮演如同 WHERE 的角色，篩選特定計算後的結果，也就是所謂的「彙總函式(Aggregate function)」。
以下例子是使用資料庫 AdventureWorksLT2012 。

``` sql
  USE AdventureWorksLT2012
  GO
  SELECT ProductID, AVG(OrderQty) AS AverageQuantity, SUM(LineTotal) AS Total
  FROM SalesLT.SalesOrderDetail
  GROUP BY ProductID
  HAVING SUM(LineTotal) > $1000
  --AND AVG(OrderQty) < 3 ;
  GO
``` 
