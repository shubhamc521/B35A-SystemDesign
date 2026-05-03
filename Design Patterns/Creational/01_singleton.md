# Singleton Design Pattern

## One Liner
Ensures that a class has only one instance and provides global access to it.

- For shared resources like configuration, logging, database. (Here resources should be shared i.e only one instance should be created)

## Example

```java

public class DatabaseConnection{
    private static DatabaseConnection instance;

    private DatabaseConnection(){}

    // Public method to provide aceess to this single
    public static DatabaseConnection getInstance(){
        if(instance == null)
        {
            instance = new DatabaseConnection();
        }
    return instance;
    }

    public void connect(){
        SOP("Connecting to database.....");
    }
}

public class Demo{
    public static void main(String[] args){
        DatabaseConnection db1 = DatabaseConnections.getInstance();

        // Get the singleton instnce again (return the same object)
        DatabaseConnection db2 = DatabaseConnections.getInstance();

        db1.connect();

        System.out.println(db1==db2); // True, same instance
    }
}
```

Here the constructor is private?
- No other class should be able to create instance directly.
- The static method getInstance() checks if an instance already exists or not, if not, create one
- All caller will get the same instance.

- new DatabaseConnection() in main ---> Compilation error.

Lazy Instantiation - [Class Load] --> [First getInstance() called] - Instance created.
                     (No memory will be utilized untill needed)

Eager Instatiation - [Class Loads] ----> Instance got created immediately
                     (Memory will be utilized even when not used)