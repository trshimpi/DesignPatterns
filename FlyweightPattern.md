### **Flyweight Design Pattern - Explanation**  

#### **1. Definition**  
The **Flyweight Pattern** is a **structural design pattern** used to **minimize memory usage** and **increase performance** by sharing common object states instead of creating new instances. It is useful when dealing with a **large number of similar objects**.  

---

#### **2. Key Concepts**  
- **Intrinsic State**: Shared, immutable data stored in the Flyweight object.  
- **Extrinsic State**: Context-specific data that is passed to the Flyweight object when needed.  
- **Flyweight Factory**: Manages and reuses Flyweight objects instead of creating new ones.  

---

#### **3. Key Components**  
1. **Flyweight Interface** – Defines the common operations for Flyweight objects.  
2. **Concrete Flyweight** – Implements the Flyweight interface and stores the intrinsic state.  
3. **Flyweight Factory** – Creates and manages Flyweight objects, ensuring object reuse.  
4. **Client** – Uses Flyweight objects and passes the extrinsic state dynamically.  

---

### **4. When to Use the Flyweight Pattern?**  
✔ When you have a **large number of objects** consuming significant memory.  
✔ When objects share **common immutable state** and only differ in small, context-specific data.  
✔ When performance and memory optimization are **critical**.  
✔ When creating objects dynamically would lead to **high memory consumption**.  

---

### **Example in Java**  
**Scenario:**  
Suppose we are designing a **text editor** where each character is an object. Instead of creating a separate object for each character, we reuse shared objects for the same character (Intrinsic state) while maintaining unique positions (Extrinsic state).  

---

#### **Step 1: Create the Flyweight Interface**
```java
// Flyweight Interface
interface CharacterFlyweight {
    void display(int fontSize, String fontColor);
}
```

#### **Step 2: Create Concrete Flyweight**
```java
// Concrete Flyweight: Represents a specific character
class Character implements CharacterFlyweight {
    private final char symbol; // Intrinsic state (shared)

    public Character(char symbol) {
        this.symbol = symbol;
    }

    @Override
    public void display(int fontSize, String fontColor) {
        System.out.println("Character: " + symbol + ", Font Size: " + fontSize + ", Font Color: " + fontColor);
    }
}
```

#### **Step 3: Create Flyweight Factory**
```java
import java.util.HashMap;
import java.util.Map;

// Flyweight Factory: Manages shared Character objects
class CharacterFactory {
    private static final Map<Character, CharacterFlyweight> characterPool = new HashMap<>();

    public static CharacterFlyweight getCharacter(char symbol) {
        characterPool.putIfAbsent(symbol, new Character(symbol));
        return characterPool.get(symbol);
    }

    public static int getTotalCharactersCreated() {
        return characterPool.size();
    }
}
```

#### **Step 4: Client Code**
```java
public class FlyweightPatternExample {
    public static void main(String[] args) {
        // Creating characters using Flyweight Factory
        CharacterFlyweight c1 = CharacterFactory.getCharacter('A');
        c1.display(12, "Red");

        CharacterFlyweight c2 = CharacterFactory.getCharacter('B');
        c2.display(14, "Blue");

        CharacterFlyweight c3 = CharacterFactory.getCharacter('A'); // Reusing 'A'
        c3.display(16, "Green");

        System.out.println("Total unique Character objects created: " + CharacterFactory.getTotalCharactersCreated());
    }
}
```

#### **Output:**
```
Character: A, Font Size: 12, Font Color: Red
Character: B, Font Size: 14, Font Color: Blue
Character: A, Font Size: 16, Font Color: Green
Total unique Character objects created: 2
```

Here, instead of creating a new object for each **'A'**, the factory reuses the same instance, optimizing memory usage.

---

### **5. Real-World Examples**
✔ **Text Rendering in IDEs** – Same characters in different styles share intrinsic data.  
✔ **Game Development** – Large sets of trees, enemies, or bullet objects are reused.  
✔ **Icons in UI Frameworks** – Common icons are stored once and reused across the application.  
✔ **Database Connection Pooling** – Connections are shared rather than creating new ones every time.  

---

### **6. Advantages & Disadvantages**
#### ✅ **Advantages**  
✔ **Memory Optimization** – Reduces RAM usage by reusing objects.  
✔ **Improved Performance** – Less object creation results in faster execution.  
✔ **Scalability** – Helps manage a large number of objects efficiently.  

#### ❌ **Disadvantages**  
✘ **Complexity** – Requires additional logic for managing shared objects.  
✘ **Not Suitable for Mutable Objects** – Works best when the intrinsic state is immutable.  

---

### **7. Conclusion**  
The **Flyweight Pattern** is ideal for reducing memory consumption when dealing with **a massive number of similar objects**. By separating **intrinsic (shared) and extrinsic (context-specific) states**, it enhances **performance and scalability**. 🚀
