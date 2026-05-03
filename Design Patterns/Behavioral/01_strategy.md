# Strategy

Swap algorithms at runtime.

# Example: 
Payment: CreditCard / UPI / Wallet

```java
public interface DiscountStrategy{
    double apply(double total);
}

public class EmployeeDiscount implements DiscountStategy{
    @Override
    public double apply(double total){
        return total * 0.8; //20% off for employee.
    }
}

public class HolidayDiscount implements DiscountStategy{
    @Override
    public double apply(double total){
        return total * 0.9; //10% off on Holidays employee.
    }
}

public class StudentDiscount implements DiscountStategy{
    @Override
    public double apply(double total){
        return total * 0.75; //25% off for students.
    }
}

public class DiscountCalculator{
    private DiscountStrategy Strategy;

    DiscountCalculator(DiscountStrategy strategy)
        {
            this.strtegy = strategy;
        }

        public double calculate(double total)
        {
            return strategy.apply(total)
        }
}

public class DemoDiscount{
    public static void main(String[] args){
        double total = 100.0;

        DiscountCalculator calc = new DiscountCalculator(new EmployeeDiscount);
        calc.calculate();

        
    }
}

