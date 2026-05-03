# Factory Design Pattern

## One Liner
Factory Design pattern provides a way to create objects without specifying the exact class of object that will be created.

It encapsulates object creation logic, making code flexible and extensible.

## Example
```java

public interface Product{
    void use();
}

// Concreate products 
public class Book implements Product{
    public void use(){
        SOP("Reading Book......");
    }
}

public class Pen implements Product{
    public void use(){
        SOP("Writting with Pen.....");
    }
}

public class ProductFactory{
    public static Product createProduct(String type){
        if(type.equals("book")) return new Book();
        if(type.equals("pen")) return new pen();
        throw new IllegalArgumentExeption("Unknow Type");
    }
}

product p1 = Productfactory.createProduct("book");
product p2 = Productfactory.createProduct("pen");

p1.use();
p2.use();










```