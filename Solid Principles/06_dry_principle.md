# DRY Principle (Don't Repeat Yourself)

## One Liner
Avoid Duplecating the code or logic.
Every peice of knowledge should have a single, unambigous representation.


## Validation Example

# Bad Code

```java
public class UserService{

        public boolean isValidEmail(String email){
            return email.contains("@") && email.endsWith(".com"); // Issue is in userService and he edits the mailchecking logic here.
        }

}

public class RegistrationController{
        public boolean isValidEmail(String email){
            return email.contains("@") && email.endsWith(".com"); // && email.contains("gmail"); // He might not edit code.
        }
}
```

# Good Code

```java

public class ValidationUtils{
    public static boolean isValidEmail(String email){
        return email.contains("@") && email.endsWith(".com"); // && email.contains("gmail")

    }
}

public class UserService{

        public boolean isValidEmail(String email){
            return ValidationUtils.isValidEmail(email);
        }

}

public class RegistrationController{
        public boolean isValidEmail(String email){
            return ValidationUtils.isValidEmail(email);
        }
}




```java