# Decorator Design Pattern

## Overview
The **Decorator Pattern** is a **structural design pattern** that allows behavior to be added to individual objects, dynamically, without modifying their code. It follows the **open-closed principle** by enabling extension without altering existing code.

## When to Use?
- When you need to **extend the functionality** of a class **dynamically** at runtime.
- When **subclassing is impractical** due to a large number of possible extensions.
- When you want to **adhere to the Single Responsibility Principle (SRP)** by separating concerns.

## Key Features
- Promotes **composition over inheritance**.
- Adds flexibility by **allowing behavior modifications at runtime**.
- Avoids **class explosion** (too many subclasses for different variations).

---

## Implementation Steps
1. **Create a Component Interface** → Defines the common methods.
2. **Implement a Concrete Component** → The base implementation.
3. **Create an Abstract Decorator** → Implements the component interface and holds a reference to a wrapped component.
4. **Implement Concrete Decorators** → Extend functionality by overriding methods.

---

## Example: Coffee Shop ☕ (Java Implementation)

### Step 1: Create the Component Interface
```java
interface Coffee {
    String getDescription();
    double cost();
}
```

### Step 2: Implement a Concrete Component
```java
class SimpleCoffee implements Coffee {
    public String getDescription() {
        return "Simple Coffee";
    }
    public double cost() {
        return 5.0;
    }
}
```

### Step 3: Create an Abstract Decorator
```java
abstract class CoffeeDecorator implements Coffee {
    protected Coffee decoratedCoffee;
    
    public CoffeeDecorator(Coffee coffee) {
        this.decoratedCoffee = coffee;
    }
    
    public String getDescription() {
        return decoratedCoffee.getDescription();
    }
    
    public double cost() {
        return decoratedCoffee.cost();
    }
}
```

### Step 4: Implement Concrete Decorators
```java
class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }
    public String getDescription() {
        return decoratedCoffee.getDescription() + ", Milk";
    }
    public double cost() {
        return decoratedCoffee.cost() + 1.5;
    }
}

class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee coffee) {
        super(coffee);
    }
    public String getDescription() {
        return decoratedCoffee.getDescription() + ", Sugar";
    }
    public double cost() {
        return decoratedCoffee.cost() + 0.5;
    }
}
```

### Step 5: Client Usage
```java
public class DecoratorPatternDemo {
    public static void main(String[] args) {
        Coffee coffee = new SimpleCoffee();
        System.out.println(coffee.getDescription() + " -> Cost: $" + coffee.cost());

        coffee = new MilkDecorator(coffee);
        System.out.println(coffee.getDescription() + " -> Cost: $" + coffee.cost());
        
        coffee = new SugarDecorator(coffee);
        System.out.println(coffee.getDescription() + " -> Cost: $" + coffee.cost());
    }
}
```

### ✅ Output
```
Simple Coffee -> Cost: $5.0
Simple Coffee, Milk -> Cost: $6.5
Simple Coffee, Milk, Sugar -> Cost: $7.0
```

---

## Advantages ✅
✔ **Follows Open-Closed Principle** → Allows extension without modifying existing code.  
✔ **Promotes Composition** → Behavior can be added dynamically.  
✔ **Reduces Subclass Explosion** → No need to create multiple subclasses for different feature combinations.  

## Disadvantages ❌
❌ **Complexity** → Can lead to multiple small objects that may be hard to manage.  
❌ **Debugging Difficulty** → Multiple wrappers make it harder to trace behavior.  

---

## Decorator Pattern vs. Other Patterns
| Pattern        | Purpose | Example |
|---------------|---------|---------|
| **Decorator** | Dynamically adds behavior | Adding features to Coffee |
| **Factory** | Creates instances | Generating Coffee objects |
| **Adapter** | Converts one interface into another | Wrapping legacy APIs |

---

## When NOT to Use Decorator Pattern?
- If **modifications are static and known at compile-time**, inheritance might be simpler.
- If the **number of decorators** becomes too high, leading to complexity.

---

## 🔥 Conclusion
The **Decorator Pattern** is a flexible way to **add responsibilities to objects dynamically**. It is widely used in **GUI frameworks, text processing, and I/O streams** (e.g., Java I/O classes). However, excessive use can lead to maintainability challenges.

Would you like notes on another pattern? 😊
