# Adapter Design Pattern (Structural Pattern)

## **Definition**

The **Adapter Pattern** is a **structural design pattern** that allows incompatible interfaces to work together by acting as a bridge between them. It translates one interface into another that the client expects, **enabling interoperability** between different systems or classes.

---

## **Key Components**

1. **Target Interface** – The interface expected by the client.
2. **Adaptee (Existing Class)** – The class with an incompatible interface that needs to be adapted.
3. **Adapter (Bridge Class)** – The class that implements the target interface and internally calls the adaptee’s methods, making them compatible.
4. **Client** – The entity that uses the adapter without knowing about the adaptee.

---

## **When to Use the Adapter Pattern?**

✔ When you want to use an existing class but its interface is incompatible with what you need.\
✔ When you need to integrate third-party libraries into your system without modifying their code.\
✔ When you want to bridge the gap between new and legacy code.\
✔ When you need to standardize multiple existing classes with different interfaces.

---

## **Example in Java**

#### **Scenario:**

We have an **old **``** class** that provides 220V power, but our **client (Mobile Charger) needs 5V**. We create an **adapter (**``**)** to convert the voltage.

```java
// Step 1: Define the Target Interface
interface Voltage5V {
    int get5V();
}

// Step 2: Define the Incompatible Adaptee Class
class Voltage220V {
    public int get220V() {
        return 220;
    }
}

// Step 3: Create the Adapter Class
class VoltageAdapter implements Voltage5V {
    private Voltage220V voltage220V;

    public VoltageAdapter(Voltage220V voltage220V) {
        this.voltage220V = voltage220V;
    }

    @Override
    public int get5V() {
        int volts = voltage220V.get220V();
        return volts / 44; // Convert 220V to 5V
    }
}

// Step 4: Client Code
public class AdapterPatternExample {
    public static void main(String[] args) {
        Voltage220V voltage220V = new Voltage220V();
        Voltage5V adapter = new VoltageAdapter(voltage220V);
        
        System.out.println("Converted Voltage: " + adapter.get5V() + "V");
        // Output: Converted Voltage: 5V
    }
}
```

---

## **Types of Adapter Patterns**

1. **Class Adapter (Using Inheritance)**
   - Adapter **extends** the adaptee class and implements the target interface.
   - Used when multiple inheritance is possible.
2. **Object Adapter (Using Composition)**
   - Adapter **contains** an instance of the adaptee class.
   - Preferred approach in Java as it follows **composition over inheritance**.

---

## **Real-World Examples**

1. **Java I/O Streams (InputStreamReader & OutputStreamWriter)**

   - `InputStreamReader` acts as an adapter between **byte streams** and **character streams**.

2. **JDBC Drivers**

   - JDBC provides a unified API for different databases by using adapters (drivers) to connect to MySQL, PostgreSQL, etc.

3. **Spring Framework Adapters**

   - `HandlerAdapter` bridges the gap between **different request handlers** in Spring MVC.

4. **Legacy System Integration**

   - Adapting an old logging system to work with a modern logging framework.

---

## **Advantages**

✔ **Allows Reusability** – Reuse existing code without modification.\
✔ **Improves Compatibility** – Makes incompatible interfaces work together.\
✔ **Follows Open/Closed Principle** – The adapter can be extended without modifying existing code.\
✔ **Enhances Code Maintainability** – Keeps client code simple by using a unified interface.

## **Disadvantages**

✘ **Increased Complexity** – Adds an extra layer between client and adaptee.\
✘ **Overhead** – Adapter processing may introduce slight performance overhead.

---

The **Adapter Pattern** is widely used in **frameworks, legacy integration, and third-party API adaptation** to ensure different systems can communicate seamlessly! 🚀

