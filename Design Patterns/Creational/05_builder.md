# Builder Design Pattern

## One Liner
Contructs complex objects step by step, allowing different representations using same construction process.

Making Laptop:

new Laptop("Inteli5", 16, NvidiaGPU, 512, Green)

Laptop l1 = new Laptop().setCPU("Intel").setGPU("Nvidia).setRAM("16").SetStorage("512").build()


```java

class Car{
    String engine;
    int wheels;
}

class CarBuilder{
    Car car = new Car();

    Carbuilder setEnginer(String e){
        car.engine = e;
        return this;
    }

    Carbuilder setWheels(String e){
        car.wheels = e;
        return this;
    }
    
    Car build(){
        return car;
    }

}

// usage
Car car = new CarBuilder.setEngine("V10").setWheels(4).build();

