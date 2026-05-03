# Adapter Design Pattern

Adapter

Android - 3.5mm audio jack - Wired Headphones

Iphone - Do not have 3.5mm jack,
         Type C                 - Type C to 3.5mm Converter - Wired headphones.
                                  ADAPTER

## Adapter Design Pattern

Adapter (also called as Wrapper) converts the interface of a class into another interface that client expects.

Its makes classes work together that are incompatible due to interfaces.

```java
interface DigitalPayment {
    void makePayment(double amount, String recipient);
}

class LegacyBankAPI{
    void trasferMoney(String fromAccount, String toAccount, double amount){

    }
}
// Adapter

class UPIAdapter implements DigitalPayment{
    private LegacyBankAPI bankAPI;
    private String upiId;


    public UPIAdapter(LegacyBankAPI bankAPI, String upiId ){
        this.bankAPI = bankAPI;
        this.upiId = upiId;
    }

    @Override
    void makePayment(double amount, String recipient){
        bankAPI.transferMoney("SendersAcc", UpiID, amount)

    }

}

// Client
DigitalPayment payment = new UPIAdapter(new LegacyBankAPI(), "user@ubl");
payment.makePayment(100.0, "merchant@Upi")


```