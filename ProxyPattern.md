# Proxy Design Pattern

## 1. Definition

The **Proxy Pattern** is a **structural design pattern** that provides a **surrogate** or **placeholder** for another object to control access to it. It acts as an intermediary between the client and the real object, often used for controlling access, adding security, or optimizing performance.

---

## 2. Key Components

1. **Subject (Interface or Abstract Class)** – Defines the common interface for the Real Object and Proxy.
2. **Real Subject (Actual Object)** – The real object that the proxy represents.
3. **Proxy** – Controls access to the real subject and may add additional functionality.
4. **Client** – Uses the subject interface to interact with the proxy.

---

## 3. When to Use the Proxy Pattern?

- When you want to **control access** to an object, such as in security-sensitive operations.
- When creating **expensive objects lazily** (e.g., database connections, file I/O).
- When implementing **caching** to avoid redundant operations.
- When adding **logging or monitoring** to method calls.
- When using **remote objects** in distributed applications (e.g., RMI, Web Services).

---

## 4. Example in Java

### **Scenario:**

We have a **Real Database Service** that fetches data. Instead of directly calling it, we introduce a **Proxy** that adds caching to optimize performance.

```java
// Step 1: Define the Subject Interface
interface DatabaseService {
    void fetchData();
}

// Step 2: Create the Real Subject (Actual Database Service)
class RealDatabaseService implements DatabaseService {
    @Override
    public void fetchData() {
        System.out.println("Fetching data from the database...");
    }
}

// Step 3: Create the Proxy Class
class DatabaseProxy implements DatabaseService {
    private RealDatabaseService realDatabaseService;
    private boolean cacheEnabled;
    
    public DatabaseProxy(boolean cacheEnabled) {
        this.cacheEnabled = cacheEnabled;
    }

    @Override
    public void fetchData() {
        if (cacheEnabled) {
            System.out.println("Returning cached data...");
        } else {
            if (realDatabaseService == null) {
                realDatabaseService = new RealDatabaseService(); // Lazy initialization
            }
            realDatabaseService.fetchData();
        }
    }
}

// Step 4: Client Code
public class ProxyPatternExample {
    public static void main(String[] args) {
        DatabaseService proxy = new DatabaseProxy(true);
        proxy.fetchData(); // Output: Returning cached data...

        DatabaseService proxyWithoutCache = new DatabaseProxy(false);
        proxyWithoutCache.fetchData(); // Output: Fetching data from the database...
    }
}
```

---

## 5. Types of Proxy Patterns

1. **Virtual Proxy** – Lazily initializes expensive objects (e.g., database connections, images).
2. **Protection Proxy** – Restricts access based on authentication (e.g., user role-based security).
3. **Remote Proxy** – Provides local access to a remote object (e.g., RMI, Web Services).
4. **Cache Proxy** – Implements caching to reduce redundant processing (e.g., database queries).
5. **Smart Proxy** – Adds extra functionalities like logging, tracking, or reference counting.

---

## 6. Real-World Examples

-  **Hibernate Lazy Loading** – Uses a proxy to load objects only when needed.
-  **Spring AOP (Aspect-Oriented Programming)** – Uses proxies to implement logging, security, and transactions.
-  **Java RMI (Remote Method Invocation)** – Uses proxies for remote method execution.
-  **Web Services (SOAP, REST)** – Clients interact with a proxy that communicates with a remote server.

---

## 7. Advantages & Disadvantages

### ✅ Advantages

- Improves **performance** with lazy initialization and caching.
- Enhances **security** by controlling object access.
- Allows **monitoring and logging** transparently.
- Supports **distributed systems** by representing remote objects. 

### ❌ Disadvantages

- Introduces **extra complexity** in code.
- Can cause **performance overhead** if used excessively.
- May **increase response time** due to additional processing.

---

## 8. Conclusion

The **Proxy Pattern** is widely used in **lazy loading, security, caching, logging, and remote method invocation**. It ensures efficient access control while keeping the client code **decoupled** from the real object! 🚀

