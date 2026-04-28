# Liskov Substitution Princliple

## One Liner
- Substypes/subclass/child class must be substitutable for their base types without altering desirable program properties.

## Concepts
- Superclass / base class : commom behavior and contract.
- Subclass /subtype : Speciacialiszed version that should follow the same contract. 


## Bad Code
```java 

//Base class: BankAccount allows deposit and withdraw.

public class BankAccount{
    protected double accountBalance;

    public BankAccount(double initialBalance){
        this.accountBalance = initialBalance;
    }

    public void deposit(double depositAmount){
        accountBalance += depositAmount;
    }

    public void withdraw(double withdrawmount){
        accountBalance -= withdrawAmount;
    }

    public double getBalace(){
        return accountBalance;
    }
}

// Fixed Account
public class FixedDepositAccount extends BankAccount {

    public FixedDeposit(double intitalBalance){
        super(initialBalance); // calls the parent class contructor with intialBalance so that base class can intialize
    }

    @override 
    public void withdraw(double withdrawAmount){
        throw new UnsupportedOperationException("Cannot withdraw from Fixed Deposit");
    }

}

// Savings Account
public class SavingsAccount extends BankAccount {

    public SavingsAccount(double intitalBalance){
        super(initialBalance); // calls the parent class contructor with intialBalance so that base class can intialize
    }

}

// Savings Account
public class CurrentAccount extends BankAccount {

    public CurrentAccount(double intitalBalance){
        super(initialBalance); // calls the parent class contructor with intialBalance so that base class can intialize
    }

}

public class BankDemo {
    public static void main(String[] args){
        BankAccount savingAccount = new SavingAccount(1000);
        savingAccount.withdraw(100); // work, balance = 900

        BankAccount currentAccount = new CurrentAccount(500);
        currentAccount.withdraw(500);

        BankAccount FixedDepositAccount = new FixedDepositAccount(2000);
        // This will throw an exception.
        fixeddepositAccount.withdraw(500); //LSP violated: Not substitutable
    }
}

```

## Good Example
```java

//Base class: BankAccount allows deposit and withdraw.

public class BankAccount{
    protected double accountBalance;

    public BankAccount(double initialBalance){
        this.accountBalance = initialBalance;
    }

    public void deposit(double depositAmount){
        accountBalance += depositAmount;
    }

    public double getBalace(){
        return accountBalance;
    }
}

// Fixed Account
public class FixedDepositAccount extends BankAccount {

    public FixedDeposit(double intitalBalance){
        super(initialBalance); // calls the parent class contructor with intialBalance so that base class can intialize
    }

}

// Savings Account
public class SavingsAccount extends BankAccount {

    public SavingsAccount(double intitalBalance){
        super(initialBalance); // calls the parent class contructor with intialBalance so that base class can intialize
    }

}

// Savings Account
public class CurrentAccount extends BankAccount {

    public CurrentAccount(double intitalBalance){
        super(initialBalance); // calls the parent class contructor with intialBalance so that base class can intialize
    }

}

public class BankDemo {
    public static void main(String[] args){
        BankAccount savingAccount = new SavingAccount(1000);
        savingAccount.withdraw(100); // work, balance = 900

        BankAccount currentAccount = new CurrentAccount(500);
        currentAccount.withdraw(500);

        BankAccount FixedDepositAccount = new FixedDepositAccount(2000);
    }
}
```
