# Chain of Responsibility

Pass request along chain of handlers until one handles it.


Request -> Handler1 -> Handler2 -> Handler3 -> null

## Example:
ATM Withdrawal: 500 note -> 200 note -> 100 note handler

```java
interface Handler {
    {
        void handle(int req);
    }
}

class A implements Handler{ //SwiggyBot
    Handler next;
    public void handle(int req){
        if(req==1)
            SOP("A handled");
    }
}

class B implements Handler{ // L1 Support guy
    Handler next;
    public void handle(int req){
        if(req==2)
            SOP("B handled");
    }
    
}


A a = new A(); //Create Handlers
B b = new B();

a.next(b); // Chain: A->B

a.handle(1); // A handles
a.handle(2); // Passes to b
a.handle(3); // No one handles





```