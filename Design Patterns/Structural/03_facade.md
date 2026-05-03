# Facade Design Pattern

Facade

- Facade provides a simplefied, unified interface to a complex subsystem.
- It makes the subsystems easier to use by hiding its complexity.

One simple interface that internally delegates to many complex objects.


## Example

```java

//Subsytems
class cpu {
    void start();
}

class Memory{
    void load();
}

class HardDrive{
    void read();
}

class Computer{
    private CPU cpu = new CPU();
    private Memory memory = new Memory();
    private HardDive hd = new HardDrive();

    void start(){
        cpu.start();
        memoey.start();
        hd.start();
    }
}

Computer comp = new Computer();
comp.start();

```