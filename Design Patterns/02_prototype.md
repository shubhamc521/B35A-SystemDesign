# Prototype 

## One Liner 
Clone exisiting objects to create new ones without depending on their concreate classses.


## Example

```java
public class AirCooler{
    String model;
    int capacityInLitres;

    public AirCooler(String moodel, int capacityInLitres){
        this.model = model;
        this.capacityInLitres = capacityInLitres;
    }

    public AirCooler clone(){
        return new AirCooler(model, capacityInLitres);
    }

    public void setCapacity(int litres){
        this.capacityInLitres = litres;
    }

}

public class Demo{
    public static void main(String[] args){
        AirCooler original = new AirCooler("CoolBreeze", 40);
        AirCooler copy = original.clone();
        copy.setCapacity(50);

        SOP(original); // CoolBreeze 40 Lit
        SOP(Copy); // CoolBreeze 50 lit 



    }
}




```