# Abstract Factory Design Pattern

## One Liner
- Provides an interfae for crating families of related or dependent objects without specifying their concrete classes.


```java
interface Book{
    void read();
}

interface Pen{
    void write();
}

// Concreate products

class EducationalBook implements Book{
    public void read(){
        SOP("EDU Book");
    }
}

class EducationalPen implements pen{
    public void write(){
        SOP("EDU Pen");
    }
}

class OfficeBook implements Book{
    public void read(){
        SOP("Office Book");
    }
}

class OfficePen implements pen{
    public void write(){
        SOP("Office Pen");
    }
}

// Abstract Factory
interface StationaryFactory{
    Book createBook();
    Pen createPen();
    }

// Concreate Factory

class EducationalFactory implements StationaryFactory{
    public book createBook(){
        return new EducationalBook();
    }
     public pen createPen(){
        return new EducationalPen();
     }
}

class OfficeFactory implements StationaryFactory{
    public book createBook(){
        return new OfficeBook();
    }
     public pen createPen(){
        return new OfficePen();
     }
}

//uSage

StationaryFactory factory = new EducationFactory();
Book book = factory.createBook();
Pen pen = factory.createPen();

```java

- Use ABstract factories only when you need to create families of related objects.