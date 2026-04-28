# Open/Closed Principle

## One - Liner
Software entities (Class, modules, functions) should be open for extension and closed for modification.

## Concept:
- Extension: adding new behavior or feature
- Modification: Changing existing code

# Bad Example

```java
public class DiscountCalculator{

    private double total;

    public DiscountCalculator(double total){
    }

    public double calculate(Customer c){
        if(c.isEmployee())
        return total * 0.8; // 20% off for employee
        if(c.isHoliday())
        return total * 0.9; // 10% off on holidays
        // if(c.Student())
        // return total * 0.75; // Student
        return total;
    }
}

```
# Good Example

- Interface: A contract that list all the methods and its signatures without the implementation.

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



```
