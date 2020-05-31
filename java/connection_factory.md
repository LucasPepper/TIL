# Connection Factory

```
public class ConnectionFactory {
    public Connection getConnection() {
        try {
            return DriverManager.getConnection(
                "jdbc:mysql://localhost/dbPepper", "user", "password");
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```