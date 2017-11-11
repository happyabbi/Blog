---
title: Python - List
categories:
- Python 3
tags:
- Python basic
---

## basic
在Python中，串列（List）是有序的物件集合，具有索引特性，長度可以變動。要建立串列，可以使用[]實字，串列中每個元素，使用逗號 , 區隔。例如：

``` Python
list1 = []
list1.append(1)
list1.append('two')
list1.append(True)
print(list1)
[1, 'two', True]

print(list1.pop())
True

print(list1)
[1, 'two']

list1.remove('two')
print(list1)
[1]

list1.insert(0, 'three')
print(list1)
['three', 1]

list2 = [1, 'two', True]
print(list2)
[1, 'two', True]
```
## operation
使用[]建立串列物件，為list的實例，若沒有指定任何元素，長度為0。你可以對串列使用append()、pop()、remove()、reverse()、sort()等方法，如果要附加多個元素，則可以使用extend()方法，
例如list1.extend([10, 20, 30])。在上例中，[1, 'two', True]建立串列物件，索引0、1、2分別為1、'two'與True，長度為3。

``` Python
list3 = ['one', 'two', 'three', 'four']
list3[0] = 1
print(list3)
[1, 'two', 'three', 'four']

list3[1:3] = [2, 3]
print(list3)
[1, 2, 3, 'four']

del list3[0]
print(list3)
[2, 3, 'four']

del list3[0:2]
print(list3)
['four']

```

## [:] 切片運算
使用[:]切片運算進行元素取代，使用list3[1:]就是清除從索引1到之後所有元素，所以list3[:] = []就相當於清空串列。

如果要測試串列的長度，可以使用len()，如果要測試某個元素是否存在於串列中，可以使用in運算子，如果要走訪整個串列，可以使用for迴圈：

``` Python
list4 = ['one', 'two', 'three', 'four']
print(len(list4))
4

print('five' in list4)
False

for elem in list4:
     print(elem)
one
two
three
four
```

## 二維
如果要模擬二維以上的串列，可以使用[]作巢狀的結構。例如：
``` Python
list5 = [[1, 2, 3], [4, 5, 6]]
for row in list5:
     for elem in row:
         print(elem)
1
2
3
4
5
6
```

注意對於串列的切片運算，並不是複製元素，而是建立一個新串列，而後將原串列中的每個元素，給新串列中指定的索引來參考。例如：

``` Python
list6 = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
i1 = list6[0:2]
print(i1)
[[1, 2, 3], [4, 5, 6]]

i1[0][1] = 20
print(i1)
[[1, 20, 3], [4, 5, 6]]

print(list6)
[[1, 20, 3], [4, 5, 6], [7, 8, 9]]
```

如果對串列使用[:]，則就相當於建立一個新串列，串列中每個索引位置皆參考到舊串列中每個索引位置的元素，也就是進行所謂的淺層複製（Shallow copy）：
``` Python
list7 = list6[:]
print(list7)
[[1, 20, 3], [4, 5, 6], [7, 8, 9]]

list7[1][2] = 60
print(list7)
[[1, 20, 3], [4, 5, 60], [7, 8, 9]]

print(list6)
[[1, 20, 3], [4, 5, 60], [7, 8, 9]]
```

## *
你可以對串列使用*，指定加倍串列的內容，注意對每個元素也是進行淺層複製：
``` Python
list8 = [[1, 2, 3], [4, 5, 6]]
list9 = list8 * 2
print(list9)
[[1, 2, 3], [4, 5, 6], [1, 2, 3], [4, 5, 6]]

list9[0][0] = 100
print(list9)
[[100, 2, 3], [4, 5, 6], [100, 2, 3], [4, 5, 6]]

print(list8)
[[100, 2, 3], [4, 5, 6]]
```
## +
你可以對串列使用+，像是串接兩個串列，但實際上這會建立新串列，長度為兩個串列的和，元素內容則為兩個串列的內容。例如：
``` Python
list10 = [1, 2]
list11 = [3, 4]
list12 = list10 + list11
print(list12)
[1, 2, 3, 4]
```

## sort
你可以對串列進行排序。例如：
``` Python
list13 = [6, 1, 7, 3, 8]
list13.sort()
print(list13)
[1, 3, 6, 7, 8]

list13.sort(reverse=True)
print(list13)
[8, 7, 6, 3, 1]
```

就初學而言，現在可以先知道，你可以對數值、字串連行比較、排序，串列中的元素必須是相同型態，在Python3中，如果串列中的型態不同，而想要進行比較、排序，則會引發例外。例如：
``` Python
list14 = ['a', 'w', 'x', 'b']
list14.sort()
print(list14)
['a', 'b', 'w', 'x']

list15 = [1, '3', 5, '2']
list15.sort()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unorderable types: str() < int()
```

如果你想從字串中取出字元，包括在串列中，則可以如下：
``` Python
print(list('Justin'))
['J', 'u', 's', 't', 'i', 'n']
```







