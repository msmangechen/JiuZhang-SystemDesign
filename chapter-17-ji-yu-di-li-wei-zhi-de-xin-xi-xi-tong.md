# Chapter 17 基于地理位置的信息系统

Q:

![](<.gitbook/assets/image (89).png>)

A: A B C



Q:

![](<.gitbook/assets/image (58).png>)

A: A B E F



Q:

![](<.gitbook/assets/image (15).png>)

A: A



Q:

![](<.gitbook/assets/image (68).png>)

A: B

所谓的按照字典序排序的意思是，从头到尾（index from 0）比较每一个字符，找到第一个不一样的字符，哪个字符更小哪个字符串就排在前面。如果其中一个是另外一个的前缀，那么前缀排在前面。如 `abc` 排在 `abcd` 的前面，`abcd` 排在 `abeg` 的前面。按照字典序排序以后，公共前缀相同的的字符串会被“挤”到一起。这是字符串排序的一个特性。



Q:

![](<.gitbook/assets/image (53).png>)

A: C



优化之前，时间复杂度是 `O(NumberOfCities * AverageFencesPerCity)`

```
for city in all_cities:
    for fence in city.all_fences:
        if check_point_in_fence(point, fence):
            return fence  
```

优化之后，时间复杂度是 `O(NumberOfCities + AverageFencesPerCity)`

```
for city in all_cities:
    if check_point_in_city(point, city):
        break
    
for fence in city.all_fences:
    if check_point_in_fence(point, fence):
        return fence
```



Q：

![](<.gitbook/assets/image (41).png>)

A：D

两个经纬度坐标很接近的位置，Google S2 的计算结果可能会相差很远。如下图：

![](<.gitbook/assets/image (38).png>)

Playground:\
[http://bit-player.org/extras/hilbert/hilbert-mapping.html](http://bit-player.org/extras/hilbert/hilbert-mapping.html)



Q：

![](<.gitbook/assets/image (66).png>)

A：D





Q：

![](<.gitbook/assets/image (37).png>)

A：D



Q：

![](<.gitbook/assets/image (84).png>)

A：B



Problems:

529

530

509



\






