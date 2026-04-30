# Single Responsibility Principle (SRP)

## One - liner
A class or module should have one, and only one, reason to change.

## Why this matters

- Class: a blueprint of objects, grouping data (fields) and behavior (methods).
- Method: a function defined inside a class
- Module: / componet: a file or package containing related classes.


# Bad Example
```java

public class Order{
    private List<string> items;

    public Order(){
        this.items = new ArrayList<>();
    }

    public void addItem(String item){
        items.add(item)
    }

    // Basiness Logic
    public double calculateTotal(){
        double total = 0.0;
        for(string item : items){
            total += 10;
        }
        return total;
    }

    public void print(){
        sop("itemlist:")
    }

    public void saveToDatabase(){
        SOP("Insert into orders")
    }

    public static void main(String[] args){
        Order o = new Order();
        o.addItem("apple");
        o.addItem("Banana")
        o.print();
        o.saveToDatabase();
    }
}
```
- Responsibilities: Saving to DB, Display

# Good Example
```java
public class Order{
    private List<string> items;

    public Order(){
        this.items = new ArrayList<>();
    }

    public void addItem(String item){
        items.add(item)
    }

    public double calculateTotal(){
        double total = 0.0;
        for(string item : items){
            total += 10;
        }
        return total;
    }

    public List<String> getitems(){
        return items;
    }
}

// Business Logic
  
public class OrderDisplay{
    public void print(List<string> items){
        sop("itemlist:")
    }
}

public class OrderRepo{
    public void saveToDatabase(List<String> items){
        SOP("Insert into orders")
    }
}
```
