---
permalink: /java/generics/
---

# Java 泛型

##  泛型参数命名约定

* E - 元素，主要由Java Collections框架使用
* K - 键，主要用于表示Map的键的参数类型
* V - 值，主要用于表示Map的值的参数类型
* N - 数字，主要表示数字
* T - 类型，主要用于表示第一个泛型类型参数
* S - 类型，主要用于表示第二个泛型类型参数
* U - 类型，主要用于表示第三个泛型类型参数
* V - 类型，主要用于表示第四个泛型类型参数



## 泛型类

### 定义格式

```java
class CustomList<E> {
  private List<E> list = new ArrayList<>();
}

class Pair<K,V> {
  private Map<K,V> map = new HashMap<>();
}

class Box<T> {
  private T t;
}

class Boxes<T,S> {
  private T t;
  private S s;
}
```



## 泛型方法

### 定义格式

```java
public <E> void printArray(E[] array){
  for(E element : array){
    System.out.printf("%s ", element)
  }
  System.out.println();
}
```



## 泛型类参数化类型

### 定义格式

```java
class Box<T> {
  private T t;
  public void setT(T t){
    this.t = t;
  }
}
```



## 有界类型参数

### 定义格式

```java
public static <T extends Comparable<T>> T max(T x, T y, T z){
  T max = x;
  if(y.compareTo(max) > 0){
    max = y;
  }
  if(z.compareTo(max) > 0){
    max = z;
  }
  return max;
}

public static <T extends Number & Comparable<T>> T max(T x, T y, T z){
  //....
  return null;
}
```



## 上界通配符

### 定义格式

```java
public static double sum(List<? extends Number> numberList){
  double sum = 0.0;
  for(Number n : numberList){
    sum += n.doubleValue();
  }
  return sum;
}
```



## 无界通配符

### 定义格式

```java
public static void print(List<?> list){
 	for(Object obj : list){
    System.out.println(obj);
  }
}
```



## 下届通配符

### 定义格式

```java
class Demo {
  public static void addCat(List<? super Cat> catList){
    //TODO
  }
  public static void main(String[] args){
    List<Animal> animalList = new ArrayList<>();
    List<Cat> catList = new ArrayList<>();
    List<RedCat> redCatList = new ArrayList<>();
    List<Dog> dogList = new ArrayList<>();
    addCat(animalList);//SUCCESS
    addCat(catList); //SUCCESS
    addCat(RedCat);//ERROR
    addCat(dogList);//ERROR
  }
}

class Animal{}
class Cat extends Animal {}
class RedCat extends Cat {}
class Dog extends Animal {}
```

