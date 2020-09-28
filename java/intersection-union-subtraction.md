---
permalink: /java/stream/intersection-union-subtraction/
---

# Java 8 Stream API 实现集合交并差

## 交集

```java
List<?> intersection(List<?> list1, List<?> list2){
  List<?> first = list1.size() > list2.size()
    							? list2 : list1;
  List<?> second = list1.size() > list2.size()
    							? list1 : list2;
  return first.stream()
    .filter(x ->second.contains(x) && second.remove(x))
    .collect(Collectors.toList());
}
```



## 并集

```java
List<?> union(List<?> list1,List<?> list2){
  List<?> first = list1.size() > list2.size()
    							? list2 : list1;
  List<?> second = list1.size() > list2.size()
    							? list1 : list2;
  List<Object> result = first.stream().filter(x -> {
            second.remove(x);
            return true;
        }).collect(Collectors.toList());
  result.addAll(list2);
  return result;
}
```



## 差集

```java
List<?> subtraction(List<?> subFrom, List<?> sub){
   return subFrom.stream().filter(x -> {
            if (sub.contains(x)) {
                sub.remove(x);
                return false;
            } else {
                return true;
            }
        }).collect(Collectors.toList());
}
```

