---
permalink: /algorithm/search/
---

# 搜索算法

## 线性搜索

线性搜索是一种非常简单的搜索算法，它是对所有项目进行逐个搜索，检查每个项目，如果照发哦匹配项，则返回该特定项目，否则搜索将继续到数据收集结束。

### Java线性搜索算法实现

```java
int lineSearch(int[] array,int element){
  for(int i = 0;i< array.length;i++){
    if(array[i] == element){
      return i;
    }
  }
  return -1;
}
```


## 二分搜索

二分搜索是基于分而治之的原理，但是数据集必须是有序的。

### Java二分搜索算法实现

```java
int binarySearch(int[] array,int element){
  int low = 0;
  int high = array.length-1;
  while(low<=high){
    int mid = low+(high-low)/2;
    if(array[mid]==element){
      return mid;
    }else if(array[mid]>element){
      high = mid-1;
    }else {
      low = mid +1;
    }
  }
  return -1;
}
```



## 插值搜索

插值搜索是二分搜索的变种，是专门处理有序递增表。

### Java插值搜索算法实现

```java
int insertSearch(int[] array,int element){
  int low = 0;
  int high = array.length -1;
  while(low<high){
    int mid = low + (element-array[low]) * (high-low) / (array[high]-arrah[low]);
    if(array[mid] == element){
      return mid;
    }else if(array[mid] > element){
      high = mid - 1;
    }else {
      low = mid + 1;
    }
    if(array[high]==element){
      return high;
    }
  }
  return -1;
}
```



## 哈希搜索

哈希搜索是指在哈希表上根据索引搜索的技术，哈希表是一种以关联方式存储数据的数据结构，在哈希表中，数据以数组的格式存储，其中每个数据值都有自己的唯一索引值，如果我们知道所需数据的索引，数据访问就会变得很快。

### Java哈希搜索算法示例

```java
int hashSearch(int[] array,int element){
  Map<Integer,Integer> map = new HashMap<>(array.length);
  for(int i = 0; i< array.length; i++){
    map.put(array[i],i);
  }
  if(map.containsKey(element)){
    return map.get(element);
  }
  return -1;
}
```

