---
permalink: /java/fork-join/
---

# Java并发 Fork-Join框架

fork-join框架允许在多个worker上中断某个任务，然后等待结果将它们组合在一起。它在很大程度上利用了多处理器计算机的能力。以下是fork-join框架中使用的核心概念和对象。

### Fork

Fork是一个过程，其中任务将自身拆分为较小的独立子任务，这些子任务可以同时执行。

#### 语法

```java
Sum left = new Sum(array, low, mid);
left.fork();
```

Sum是RecursiveTask的子类，left.fork（）将任务拆分为子任务。

### Join

Join 是一个过程，在此过程中，一旦子任务完成执行，任务就会Join所有子任务的结果，否则它将一直等待。

#### 语法

```java
left.join();
```

left是Sum类的对象。

### ForkJoinPool

它是一个特殊的线程池，旨在与fork-and-join任务拆分一起使用。

#### 语法

```java
ForkJoinPool forkJoinPool = new ForkJoinPool(4);
```

这是一个并行度为4个CPU的新ForkJoinPool。

### RecursiveAction

RecursiveAction表示不返回任何值的任务。

#### 语法

```java
class Writer extends RecursiveAction {
  @Override
  protected void computed(){}
}
```

### RecursiveTask

RecursiveTask表示一个返回值的任务。

#### 语法

```java
class Sum extends RecursiveTask<Long> {
  @Override
  protected Long computed(){
    return null;
  }
}
```

#### 示例：

以下TestThread程序显示了在基于线程的环境中Fork-Join框架的用法。

```java
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ForkJoinPool;
import java.util.concurrent.RecursiveTask;

public class TestThread {
  public static void main(String[] args) throws ExecutionException{
    int nThreads = Runtime.getRuntime().avaiableProcessors();
    int[] nums = new int[1000];
    for (int i = 0; i < 1000; i++){
      nums[i] = i;
    }
    ForkJoinPool pool = new ForkJoinPool(nThreads);
    Long result = pool.invoke(new Sum(nums,0,nums.length));
    System.out.println(result);
  }
  
  static class Sum extends RecursiveTask<Long> {
    int low;
    int high;
    int[] array;
    Sum(int[] array,int low,int high){
      this.array = array;
      this.low = low;
      this.high = high;
    }
    @Override
    protected Long compute(){
      if(high-low <= 10){
        long sum = 0;
        for(int i=low;i<high; i++){
          sum +=array[i];
        }
        return sum;
      }else {
        int mid = low + (high-low) / 2;
        Sum left = new Sum(array,low,mid);
        Sum right = new Sum(array,mid,high);
        left.fork();
        long rightResult = right.compute();
        long leftResult = left.join();
        return leftResult + rightResult;
      }
    }
  }
}
```

