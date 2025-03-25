# Flyweight Design Pattern

## Overview
The **Flyweight Pattern** is a **structural design pattern** used to **reduce memory usage** and **increase performance** by sharing common object state instead of creating multiple instances of identical objects.

## When to Use?
- When a large number of **similar objects** exist in the system.
- When object creation is **memory-intensive** and must be minimized.
- When objects can be **split into intrinsic (shared) and extrinsic (unique) states**.

## Key Features
- **Minimizes memory usage** by sharing objects.
- Uses **factories** to manage shared instances.
- **Intrinsic state** (shared data) remains constant across objects.
- **Extrinsic state** (unique data) is supplied externally at runtime.

---

## Implementation Steps
1. **Create the Flyweight Interface** → Defines the method(s) for concrete flyweights.
2. **Implement Concrete Flyweight** → Implements the shared behavior and stores intrinsic state.
3. **Create a Flyweight Factory** → Manages shared instances and returns existing objects when available.
4. **Use the Flyweight in the Client** → Avoids creating duplicate objects by using the factory.

---

## Example: Tree Rendering in a Forest 🌲
Imagine a **forest** where many trees exist. Instead of creating separate tree objects, we share common attributes (e.g., tree type, texture, color) while maintaining unique positions.

### Step 1: Create the Flyweight Interface
```java
interface Tree {
    void display(int x, int y);
}
```

### Step 2: Implement the Concrete Flyweight
```java
class TreeType implements Tree {
    private final String name;
    private final String color;
    private final String texture;
    
    public TreeType(String name, String color, String texture) {
        this.name = name;
        this.color = color;
        this.texture = texture;
    }
    
    @Override
    public void display(int x, int y) {
        System.out.println("Displaying " + name + " at (" + x + ", " + y + ") with color " + color);
    }
}
```

### Step 3: Implement the Flyweight Factory
```java
import java.util.HashMap;
import java.util.Map;

class TreeFactory {
    private static final Map<String, TreeType> treeTypes = new HashMap<>();
    
    public static TreeType getTreeType(String name, String color, String texture) {
        String key = name + "-" + color + "-" + texture;
        if (!treeTypes.containsKey(key)) {
            treeTypes.put(key, new TreeType(name, color, texture));
            System.out.println("Creating new TreeType: " + key);
        }
        return treeTypes.get(key);
    }
}
```

### Step 4: Use Flyweight in the Client
```java
class Forest {
    public static void main(String[] args) {
        Tree tree1 = TreeFactory.getTreeType("Oak", "Green", "Smooth");
        tree1.display(10, 20);
        
        Tree tree2 = TreeFactory.getTreeType("Oak", "Green", "Smooth");
        tree2.display(30, 40);
        
        Tree tree3 = TreeFactory.getTreeType("Pine", "Dark Green", "Rough");
        tree3.display(50, 60);
    }
}
```

### ✅ Output
```
Creating new TreeType: Oak-Green-Smooth
Displaying Oak at (10, 20) with color Green
Displaying Oak at (30, 40) with color Green
Creating new TreeType: Pine-Dark Green-Rough
Displaying Pine at (50, 60) with color Dark Green
```

---

## Advantages ✅
✔ **Reduces memory usage** by sharing objects.  
✔ **Improves performance** by avoiding repeated object creation.  
✔ **Supports large-scale applications** like rendering trees, icons, or game objects.

## Disadvantages ❌
❌ **Complexity increases** due to managing shared instances.  
❌ **Not useful if objects have too many unique attributes**, making sharing ineffective.

---

## Real-World Examples 🌎
- **Text Editors** → Character glyphs are shared instead of creating new ones for each letter.
- **GUI Applications** → Icons and UI components are reused.
- **Games** → Rendering thousands of similar objects (e.g., trees, NPCs).
- **Database Connection Pooling** → Reusing database connections.

---

## When NOT to Use Flyweight Pattern?
- When **objects have unique state**, making sharing impractical.
- When **object creation is cheap** and memory optimization isn't critical.

---

## 🔥 Conclusion
The **Flyweight Pattern** optimizes memory usage by **sharing common object state**. It is widely used in applications requiring **large-scale object rendering** like **graphics, UI elements, and games**. However, improper use can add **unnecessary complexity**.

Would you like notes on another pattern? 😊
