---
permalink: /algorithm/sort/
---

# 排序算法

## 冒泡排序

冒泡排序是一种基本排序算法，是通过重复交换相邻元素实现的。这是所有排序算法中最基本的技术。

* 时间复杂度O(n<sup>2</sup>)
* 稳定排序
* 不适用于大型数据集

### Java冒泡排序算法实现

```java
void bubbleSort(int[] array){
  for(int i = array.length-1;i>0;i--){
    for(int j = 1; j <=i; j++){
      if(array[j]< array[j-1]){
        int temp = array[j];
        array[j] = array[j-1];
        array[j-1]=temp;
      }
    }
  }
}
```

### 示例：

| 未排序序列 | 14   | 33   | 27   | 35   | 10   |
| ---------- | ---- | ---- | ---- | ---- | ---- |
| 第一次迭代 | 14   | 27   | 33   | 10   | 35   |
| 第二次迭代 | 14   | 27   | 10   | 33   | 35   |
| 第三次迭代 | 14   | 10   | 27   | 33   | 35   |
| 第四次迭代 | 10   | 14   | 27   | 33   | 35   |

***



## 插入排序

插入排序是一种非常简单的排序方法，可以对数字进行升序或者降序排序。该方法采用增量方式，就如同玩游戏时对牌进行排序。

* 时间复杂度O(n<sup>2</sup>)
* 稳定排序
* 不适用于大型数据集

### Java插入排序算法实现

```java
void insertSort(int[] array){
  for(int i = 1; i < array.length; i++){
    int index = i;
    int current = array[index];
    while(index > 0 && current < array[index-1]){
      array[index] = array[index-1];
      index--;
    }
    array[index] = current;
  }
}
```

### 示例：

| 未排序序列 | 14   | 33   | 27   | 35   | 10   |
| ---------- | ---- | ---- | ---- | ---- | ---- |
| 第一次迭代 | 14   | 33   | 27   | 35   | 10   |
| 第二次迭代 | 14   | 27   | 33   | 35   | 10   |
| 第三次迭代 | 14   | 27   | 33   | 35   | 10   |
| 第四次迭代 | 10   | 14   | 27   | 33   | 35   |

***



## 选择排序

选择排序是基本排序技术之一，它是通过对元素进行重新排序而起作用。原理如下：首先在数组中找到最小的元素，然后与位于第一个位置的元素交换，然后找到第二个最小元素，并将其与位于第二个位置的元素交换，以此内推，直到整个数组排序完成。

* 时间复杂度O(n<sup>2</sup>)
* 不稳定排序
* 不适用于大型数据集

### Java选择排序算法实现

```java
void selectSort(int[] array){
  for(int i = 0; i < array.length-1; i++){
    int min = i;
    for(int j = i+1; j < array.length; j++){
      if(array[j] < array[min]){
        min = j;
      }
    }
    if(min != i){
      int temp = array[i];
      array[i] = array[min];
      array[min] = temp;
    }
  }
}
```

### 示例：

| 未排序序列 | 14   | 33   | 27   | 35   | 10   |
| ---------- | ---- | ---- | ---- | ---- | ---- |
| 第一次迭代 | 10   | 33   | 27   | 35   | 14   |
| 第二次迭代 | 10   | 14   | 27   | 35   | 33   |
| 第三次迭代 | 10   | 14   | 27   | 35   | 33   |
| 第四次迭代 | 10   | 14   | 27   | 33   | 35   |

***



## 希尔排序

希尔排序是一种高效的排序算法，它基于插入排序算法。

* 时间复杂度O(n)
* 不稳定排序
* 适用于中性数据集

### Java希尔排序算法实现

```java
void shellSort(int[] array){
  int interval = 1;
  while(interval < array.length / 3){
    interval = interval * 3 + 1;
  }
  while(interval > 0){
    for(int i = interval; i< array.length;i++){
      int index = i;
      int value = array[index];
      while((index>interval-1) && value < array[index-interval]){
        array[index] = array[index-interval];
        index = index-interval;
      }
      array[index] = value;
    }
    interval = (interval-1) / 3;
  }
}
```

### 示例：

| 未排序序列 | 14   | 33   | 27   | 10   | 35   | 19   | 42   | 44   |
| ---------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 第一次迭代 | 14   | 19   | 27   | 10   | 35   | 33   | 42   | 44   |
| 第二次迭代 | 10   | 14   | 19   | 27   | 33   | 35   | 42   | 44   |

***



## 快速排序

快速排序采用分治法实现，是一种很好的通用排序技术，在执行过程中消耗相对较少的资源，是大部分情况下的首选算法。

* 时间复杂度O(nLogn)
* 不稳定排序
* 适用于大型数据集

### Java快速排序算法实现

```java
void quickSort(int[] array,int low,int high){
  if(high - low > 0){
    int mid = sort(array,low,high);
    quickSort(array,low,mid-1);
    quickSort(array,mid+1,high);
  }
}
void sort(int[] array, int low, int high){
  int highVal = array[high];
  int right = high-1;
  while(true){
	  while(low < high && array[low] < highVal){
	    low++;
	  }
	  while(right > 0 && array[right] > highVal){
	    right--;
	  }
 	 if(low >= right){
  	  break;
 	 }else{
     int temp = array[low];
     array[low] = array[right];
     array[right] = temp;
   }
  }
  array[high] = array[low];
  array[low] = highVal;
  return low;
}
```

### 示例：

| 未排序序列 | 14   | 33   | 27   | 35   | 10   |
| ---------- | ---- | ---- | ---- | ---- | ---- |
| 第一次迭代 | 10   | 33   | 27   | 35   | 14   |
| 第二次迭代 | 10   | 14   | 27   | 35   | 33   |
| 第三次迭代 | 10   | 14   | 27   | 33   | 35   |

***



## 基数排序

基数排序属于分配式排序，又称“桶子法”，它是通过键值的部分信息，将要排序的元素分配至某些“桶”中完成的。

* 时间复杂度O(nlog<sub>r</sub>m)，r为采用的基数，m为堆数
* 稳定排序
* 不适用于大型数据集

### Java技术排序算法实现

```java
void radixSort(int[] array,int radix){
  int[][] temp = new int[10][array.length];
  int[] order = new int[10];
  int m = 1;
  int n = 1;
  while(m <= radix){
    for(int i = 0; i < array.length; i++){
      int lsd = array[i] / n % 10;
      temp[lsd][order[lsd]] = array[i];
      order[lsd]++;
    }
    int k=0;
    for(int i = 0; i< 10;i++){
      if(order[i] != 0){
        for(int j=0;j<order[i];j++){
          array[k++]=temp[i][j];
        }
      }
      order[i]=0;
    }
    n *= 10;
    m++;
  }
}
```

### 示例：

| 未排序序列 | 14   | 33   | 27   | 35   | 10   |
| ---------- | ---- | ---- | ---- | ---- | ---- |
| 第一次迭代 | 10   | 33   | 14   | 35   | 27   |
| 第二次迭代 | 10   | 14   | 27   | 33   | 35   |

***



## 归并排序

归并排序是一种基于分而治之的排序技术，最坏情况下的时间复杂度是O(nLogn)。

* 时间复杂度O(nLogn)
* 稳定排序
* 需要消耗额外的空间

### Java归并排序算法实现

```java
int[] mergeSort(int[] array){
  int length = array.length;
  if(length == 1){
    return array;
  }
  int left = length / 2;
  int right = length - left;
  int[] leftArray = new int[left];
  int[] rightArray = new int[right];
  System.arraycopy(array,0,leftArray,0,left);
  System.arraycopy(array,left,rightArray,0,right);
  leftArray = mergeSort(leftArray);
  rightArray = mergerSort(rightArray);
  return merge(leftArray,rightArray);
}
int[] merge(int[] left,int[] right){
  int[] array = new int[left.length+right.length];
  int i=0,j=0,k=0;
  while(i<left.length && j<right.length){
    if(left[i]>right[j]){
      array[k++] = right[j++];
    }else {
      array[k++] = left[i++];
    }
  }
  while(i<left.length){
    array[k++] = left[i++];
  }
  while(j<right.length){
    array[k++] = right[j++];
  }
  return array;
}
```

***

