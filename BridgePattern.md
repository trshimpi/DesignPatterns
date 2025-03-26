#  Bridge Design Pattern (Structural Dessign Pattern)

##  1. Definition  
The **Bridge Pattern** is a **structural design pattern** that **decouples abstraction from implementation**, allowing them to evolve independently. It achieves this by introducing an interface as a **bridge** between abstraction and concrete implementations.

---

##  2. Key Concepts  
- Separates **abstraction** (high-level logic) from **implementation** (low-level details).  
- Uses **composition** instead of inheritance, promoting flexibility.  
- Allows **extending functionality** without modifying existing code.  

---

##  3. Key Components  
1. **Abstraction** – The high-level interface that defines the core functionality and delegates tasks to Implementor.  
2. **Implementor (Bridge)** – An interface that defines the operations implemented by concrete classes.  
3. **Concrete Implementor** – Provides specific implementations of the Implementor interface.  
4. **Refined Abstraction** – Extends the Abstraction class and provides additional functionality.  

---

##  4. When to Use the Bridge Pattern?  
✔ When you need to **decouple abstraction from implementation** for better flexibility.  
✔ When you want to **avoid a deep inheritance hierarchy** that makes code rigid.  
✔ When both **abstraction and implementation** are expected to evolve independently.  
✔ When you want to **reduce code duplication** by separating logic into different classes.  

---

##  5. Real-World Example: Remote Control & Devices  
Imagine you have a **universal remote control** that can operate **different types of devices** like **TVs, Radios, or Projectors**.  

🔹 Instead of creating separate remotes for each device (`TVRemote`, `RadioRemote`, `ProjectorRemote`), we use the **Bridge Pattern** to separate the **remote control (abstraction)** from the **device (implementation)**.  

---

###  **Step 1: Create the Implementor Interface (Device)**
```java
// Implementor: Defines a general interface for all devices
interface Device {
    void turnOn();
    void turnOff();
}
```

###  **Step 2: Create Concrete Implementors (TV & Radio)**
```java
// Concrete Implementor 1: TV
class TV implements Device {
    public void turnOn() { System.out.println("TV is now ON"); }
    public void turnOff() { System.out.println("TV is now OFF"); }
}

// Concrete Implementor 2: Radio
class Radio implements Device {
    public void turnOn() { System.out.println("Radio is now ON"); }
    public void turnOff() { System.out.println("Radio is now OFF"); }
}
```

###  **Step 3: Create the Abstraction (Remote Control)**
```java
// Abstraction: Remote Control
abstract class RemoteControl {
    protected Device device;  // Bridge to Device

    protected RemoteControl(Device device) {
        this.device = device;
    }

    abstract void turnOn();
    abstract void turnOff();
}
```

###  **Step 4: Create Refined Abstraction (Advanced Remote)**
```java
// Refined Abstraction: Advanced Remote with Extra Features
class AdvancedRemote extends RemoteControl {
    public AdvancedRemote(Device device) {
        super(device);
    }

    public void turnOn() { device.turnOn(); }
    public void turnOff() { device.turnOff(); }

    // Extra Feature: Mute
    public void mute() { System.out.println("Muting the device"); }
}
```

###  **Step 5: Client Code**
```java
public class BridgePatternExample {
    public static void main(String[] args) {
        // Create a TV and control it with an Advanced Remote
        RemoteControl tvRemote = new AdvancedRemote(new TV());
        tvRemote.turnOn();
        tvRemote.turnOff();

        // Create a Radio and control it with an Advanced Remote
        RemoteControl radioRemote = new AdvancedRemote(new Radio());
        radioRemote.turnOn();
        radioRemote.turnOff();
    }
}
```

### ** Output**
```
TV is now ON
TV is now OFF
Radio is now ON
Radio is now OFF
```

---

##  6. Another Example: **Shape Drawing System**
Here, we separate **Shapes (Circle, Square, etc.)** from **Rendering methods (Vector, Raster)**.

###  **Implementor (Bridge)**
```java
interface DrawingAPI {
    void drawCircle(int radius, int x, int y);
}
```

###  **Concrete Implementors**
```java
class VectorDrawing implements DrawingAPI {
    public void drawCircle(int radius, int x, int y) {
        System.out.println("Vector Drawing: Circle with radius " + radius + " at (" + x + "," + y + ")");
    }
}

class RasterDrawing implements DrawingAPI {
    public void drawCircle(int radius, int x, int y) {
        System.out.println("Raster Drawing: Circle with radius " + radius + " at (" + x + "," + y + ")");
    }
}
```

###  **Abstraction (Shape)**
```java
abstract class Shape {
    protected DrawingAPI drawingAPI;

    protected Shape(DrawingAPI drawingAPI) {
        this.drawingAPI = drawingAPI;
    }

    public abstract void draw();
}
```

###  **Refined Abstraction (Circle)**
```java
class Circle extends Shape {
    private int radius, x, y;

    public Circle(int radius, int x, int y, DrawingAPI drawingAPI) {
        super(drawingAPI);
        this.radius = radius;
        this.x = x;
        this.y = y;
    }

    public void draw() {
        drawingAPI.drawCircle(radius, x, y);
    }
}
```

###  **Client Code**
```java
public class BridgePatternExample {
    public static void main(String[] args) {
        Shape vectorCircle = new Circle(5, 10, 10, new VectorDrawing());
        vectorCircle.draw();

        Shape rasterCircle = new Circle(7, 20, 20, new RasterDrawing());
        rasterCircle.draw();
    }
}
```

### ** Output**
```
Vector Drawing: Circle with radius 5 at (10,10)
Raster Drawing: Circle with radius 7 at (20,20)
```

---

##  7. Real-World Applications  
✔ **GUI Frameworks (Swing, JavaFX)** – Where components (abstraction) are separated from rendering engines (implementation).  
✔ **Database Drivers (JDBC)** – Provides abstraction for different database connections.  
✔ **Remote Control Devices** – A TV remote (abstraction) can control multiple brands/models of TVs (implementations).  

---

##  8. Advantages & Disadvantages  
###  **Advantages**  
✔ Improves **code flexibility** by decoupling abstraction from implementation.  
✔ **Promotes composition over inheritance**, avoiding deep class hierarchies.  
✔ Helps in maintaining **Open-Closed Principle** by allowing independent extension.  

###  **Disadvantages**  
✘ **Increased complexity** due to additional abstraction layers.  
✘ **Requires extra classes**, leading to a slightly higher maintenance cost.  

---

##  9. Conclusion  
The **Bridge Pattern** is useful when you need to separate an **abstraction from its implementation** to **allow independent changes**. It promotes a more **flexible and scalable** design. 🚀

---
