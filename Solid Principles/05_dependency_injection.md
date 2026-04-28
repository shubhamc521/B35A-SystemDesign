# Dependency Injection Principle

## One Liner 
High Level modules should not be dependent on low level module; both should should be depend on abstraction.
Abstraction should not depend on details - details should depend on abstraction.


Ecommerce Site ---> Payment - UPI, CC, DB

High Level Module - Auth Service
Low Level Module: Mailer1

# Bad Code

```java 
public class GoogleMailer{
    public void send(String to, String body){
        SOP("Sending email........");
    }
}

public class AuthService{
    // Bad - It is creating the gmailer itself.
    private GoogleMailer gmailer = new GoogleMailer(); // Direct mailer instantiation

    public void register(String emial){
        gmail.mail(email,"Welcome");
    }
}
```
Why this is bad?
- If have to onboard different mailer.
   Edit the AuthService.

# Good Code

```java 
public interface Mailer{
    public void send(String to, String body);
}

public class Gmailer implements Mailer{
    @Override
    public void send(String to, String body){
        SOP("Sending email");
    }
}

public class AuthService{
    private Mailer mailer;

    // Contructor Injection // Accepting the outside world.
    public AuthService(Mailer mailer){
        this.mailer = mailer;
    }

    public void register(String email){
        mailer.send(email, "Welcome")
    }
}

Public class DemoAuth{
    public static void main(String[] args){
        Mailer gmailer = new gmailer();
        AuthService src = new AuthService(gmailer); //Dependency is being injected here
        srv.register("abc@gmail.com");
    }
}
```
- AuthService doen't need to create gmailer itself
- Receving it from the contructor
- Dependency Injection - Dependency Injected from Outside world.