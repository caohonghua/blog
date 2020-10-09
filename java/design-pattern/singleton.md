---
permalink: /java/design-pattern/singleton/
---


# 单例模式

单例模式是Java中最简单的设计模式之一。这种设计模式属于创建模式，因为该模式提供了创建对象的最佳方法之一。

该模式涉及单个类，该类负责创建对象，同时确保仅创建单个对象。此类提供了一种访问其唯一对象的方法，该对象可以直接访问而无需实例化该类的对象。

## 实现方式

1. 懒汉式、线程不安全

   ```java
   public class Singleton {
     private static Singleton instance;
     private Singleton() {}
     public static Singletong getInstance() {
       if(instance == null) {
         instance = new Singleton();
       }
       return instance;
     }
   }
   ```

2. 懒汉式、线程安全

   ```java
   public class Singleton {
     private static Singleton instance;
     private Singleton(){}
     public static synchronized Singleton getInstance(){
       if(instance == null){
         instance = new Singleton();
       }
       return instance;
     }
   }
   ```

3. 饿汉式

   ```java
   public class Singleton{
     private static Singleton instance = new Singleton();
     private Singleton(){}
     public static Singleton getInstance(){
       return instance;
     }
   }
   ```

4. 双检索/双重校验锁（DCL）

   ```java
   public class Singleton{
     private volatile static Singleton instance;
     private Singleton(){}
     public static Singleton getInstance(){
       if(instance == null){
         sychronized(Singleton.class){
           if(instance == null){
             instance = new Singleton();
           }
         }
       }
       return instance;
     }
   }
   ```

5. 静态内部类

   ```java
   public class Singleton {
     private static class SingletonHolder {
       private static final Singleton INSTANCE = new Singleton();
     }
     private Singleton(){}
     public static final Singleton getInstance(){
       return SingletonHolder.INSTANCE;
     }
   }
   ```

6. 枚举

   ```java
   public enum Singleton {
     INSTANCE;
   }
   ```

   