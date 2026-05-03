# Bridge

Bridge lets you change "How" something works without changing "What" it does.

Bridge decouples an abstraction from its implementation so that the two can vary independently, it seperates "what" something does from "how" it does.

Abstraction: Connection , Statement interfaces - What db operations to perform.
Implementation: MySQL driver, postgresSQL driver


```java
interface Connection{
    Statement createStatement();
}

interface Statement{
    Result executeQuery(String sql);
}

interface Driver{
    Connection connect(string url);
}

// Concreate implementation
class MySQLDriver implements Driver{
    public Conncetion connect(string url){
        return new MySQLConnection();
    }
}

class PostgresSQLDriver implements Driver{
    public Conncetion connect(string url){
        return new PostgresSQLConnection();
    }
}

Driver driver = new MySQLDriver(); // Change to PostgresSQLDriver
Connection conn = driver.connect("jdbc:mysql://localhost/db");
Statement stml = conn.createStatements



```