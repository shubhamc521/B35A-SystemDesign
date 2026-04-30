# Interface  Segregation

## One Liner
Client should not be forced to depend upon interfaces they do not use.

- Interface: A contract that list methods a class should provide.

- if an interface groups unrelated methods, it becomes hard to follow the contract and implement non required methods as well or throw.

Bank Account --> Deposit and Withdraw. --> Savings Account, Current AC, and Fixed Deposit (Withdraw method exception)

Seprate the bank Account Interface into Interface:
WithDrawableAC
NonWithDrawableAC

# Bad Example
```java 
//Machine.java

public interface Machine{
    void print(Document d);
    void scan(Document d);
    void fax(Document d);
}

public class OldPrinter implements Machine{
    @Override
    public void print(Document d){
        SOP("Printing.....")
    }

    @Override
    public void scan(Document d){
        throw new UnssportedOperationException("Scan not supported.....");
    }

    @Override
    public void Fax(Document d){
        throw new UnssportedOperationException("Fax not supported.....");
    }
}

// Client Code

public class PrintDemo{
    public static void main(String[] args){
        Machine p = new OldPrinter();
        p.print(new Document("Hello"));
        //p.scan(....) throw errow
    }
}
```
Call to scan gives exception
Client is not happy as they are exception.
Developers are not happy - as they need to implement irrelevant methods.


# Good Code
```java

// Small Interfaces

public interface Printer{ void print(Document d ); }
public interface Scanner{ void scan(Document d ); }
public interface Fax{ void Fax(Document d ); }

public class AllInOnePrinter implements Printer, Scanner, Fax{
    @Override
    public void print(Document d){
        SOP("Printing.....");
    }

    @Override
    public void scan(Document d){
        SOP("Scanning....");
    }

    @Override
    public void Fax(Document d){
        SOP("Fax.....");
    }
}

public class OldPrinter implements Printer{
    @Override
    public void print(Document d){
        SOP("Printing.....")
    }
}

public class Demo{
    public static void main(String[] args){
        Document doc = new Document("Hi");

        //Client 1: only printer
        Printer simplePrinter = new OldPrinter();
        simplePrinter.print(doc);

        //Client 2: Need ALLINONE Printer
        Printer AIOPrinter - new AllInOnePrinter();
        AIOPrinter.print(doc);
        AIOPrinter.scan(doc);
        AIOPrinter.fax(doc);

        // Seperate Printer and Scanner
        Scaaner Scanner = AIOPrinter;
        AIOPrinter.scan(doc);
    }
}





```
