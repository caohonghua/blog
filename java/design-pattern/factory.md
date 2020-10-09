---
permalink: /java/design-pattern/factory/
---

# 工厂模式
工厂模式是Java中最常用的设计模式之一。这种设计模式属于创建模式，因为该模式提供了创建对象的最佳方法之一。

在Factory模式中，我们在不向客户端公开创建逻辑的情况下创建对象，并使用公共接口引用新创建的对象。

### 示例
* 创建接口
```java
public interface Shape {
    void draw();
}
```

* 创建实现相同接口的具体类

```java
public class Rectangle implements Shape {
    @Override
    public void draw(){
        System.out.println("Inside Rectangle:: draw() method.");
    }
}

public class Square implements Shape {
    @Override
    public void draw(){
        System.out.println("Inside Square:: draw() method.");
    }
}

public class Circle implements Shape {
    @Override
    public void draw(){
        System.out.println("Inside Circle:: draw() method.");
    }
}
```

* 创建工厂类，根据特定信息生成特定类

```java
public class ShapeFactory {
    public Shape getShape(String shapeType){
        if(shapeType == null){
            return null;
        }
        if("CIRCLE".equalsIgnoreCase(shapeType)){
            return new Circle();
        }
        if("SQUARE".equalsIgnoreCase(shapeType)){
            return new Square();
        }
        if("RECTANGLE".equalsIgnoreCase(shapeType)){
            return new Rectangle();
        }
        return null;
    }
}
```

* 使用示例

```java
public class ShapeFactoryDemo {
    public static void main(String[] args){
        ShapeFactory factory = new ShapeFacotry();

        Shape circle = factory.getShape("circle");
        circle.draw();

        Shape square = factory.getShape("square");
        square.draw();

        Shape rectangle = factory.getShape("rectangle");
        rectangle.draw();
    }
}
```