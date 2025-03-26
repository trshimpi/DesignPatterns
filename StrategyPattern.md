
# 🏗️ Strategy Design Pattern - Complete Guide

## 📌 1. Definition  
The **Strategy Pattern** is a **behavioral design pattern** that **defines a family of algorithms**, encapsulates each one, and makes them interchangeable. It allows the algorithm to be selected at runtime.

---

## 🔑 2. Key Concepts  
- Encapsulates different **strategies (algorithms)** in separate classes.  
- Uses **composition** instead of inheritance for flexibility.  
- Clients can **switch algorithms dynamically** at runtime.  

---

## 🏛 3. Key Components  
1. **Strategy (Interface)** – Defines a common interface for all strategies.  
2. **Concrete Strategies** – Implement different variations of the algorithm.  
3. **Context** – Uses a strategy and allows it to be changed at runtime.  

---

## ❓ 4. When to Use the Strategy Pattern?  
✔ When you have **multiple ways of performing an operation** (e.g., sorting, payment methods).  
✔ When you want to **change an algorithm dynamically at runtime**.  
✔ When using **if-else or switch-case becomes too complex**.  
✔ When different classes share similar behaviors but need **different implementations**.  

---

## 📌 5. Real-World Example: Payment Processing System  
Imagine an **e-commerce platform** where users can **pay using different methods** like **Credit Card, PayPal, or Bitcoin**. Instead of using multiple `if-else` statements, we use the **Strategy Pattern** to define a flexible and scalable solution.

---

### ✅ **Step 1: Create the Strategy Interface (Payment Strategy)**
```java
// Strategy: Common interface for all payment methods
interface PaymentStrategy {
    void pay(int amount);
}
```

### ✅ **Step 2: Implement Concrete Strategies (Credit Card, PayPal, Bitcoin)**
```java
// Concrete Strategy 1: Credit Card Payment
class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;

    public CreditCardPayment(String cardNumber) {
        this.cardNumber = cardNumber;
    }

    public void pay(int amount) {
        System.out.println("Paid $" + amount + " using Credit Card: " + cardNumber);
    }
}

// Concrete Strategy 2: PayPal Payment
class PayPalPayment implements PaymentStrategy {
    private String email;

    public PayPalPayment(String email) {
        this.email = email;
    }

    public void pay(int amount) {
        System.out.println("Paid $" + amount + " using PayPal: " + email);
    }
}

// Concrete Strategy 3: Bitcoin Payment
class BitcoinPayment implements PaymentStrategy {
    private String walletAddress;

    public BitcoinPayment(String walletAddress) {
        this.walletAddress = walletAddress;
    }

    public void pay(int amount) {
        System.out.println("Paid $" + amount + " using Bitcoin Wallet: " + walletAddress);
    }
}
```

### ✅ **Step 3: Create the Context Class (Shopping Cart)**
```java
// Context: Shopping Cart that uses different payment strategies
class ShoppingCart {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void checkout(int amount) {
        if (paymentStrategy == null) {
            throw new IllegalStateException("Payment strategy not set!");
        }
        paymentStrategy.pay(amount);
    }
}
```

### ✅ **Step 4: Client Code**
```java
public class StrategyPatternExample {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        // Pay using Credit Card
        cart.setPaymentStrategy(new CreditCardPayment("1234-5678-9012-3456"));
        cart.checkout(100);

        // Switch to PayPal payment
        cart.setPaymentStrategy(new PayPalPayment("user@example.com"));
        cart.checkout(75);

        // Switch to Bitcoin payment
        cart.setPaymentStrategy(new BitcoinPayment("1BTCWalletAddressXYZ"));
        cart.checkout(200);
    }
}
```

### **🔹 Output**
```
Paid $100 using Credit Card: 1234-5678-9012-3456
Paid $75 using PayPal: user@example.com
Paid $200 using Bitcoin Wallet: 1BTCWalletAddressXYZ
```

---

## 🔗 6. Another Example: **Sorting Algorithms**
Imagine a sorting system where users can **choose different sorting strategies** at runtime.

### ✅ **Sorting Strategy Interface**
```java
interface SortingStrategy {
    void sort(int[] numbers);
}
```

### ✅ **Concrete Sorting Strategies**
```java
// Bubble Sort
class BubbleSort implements SortingStrategy {
    public void sort(int[] numbers) {
        System.out.println("Sorting using Bubble Sort...");
        // Implement Bubble Sort logic
    }
}

// Quick Sort
class QuickSort implements SortingStrategy {
    public void sort(int[] numbers) {
        System.out.println("Sorting using Quick Sort...");
        // Implement Quick Sort logic
    }
}

// Merge Sort
class MergeSort implements SortingStrategy {
    public void sort(int[] numbers) {
        System.out.println("Sorting using Merge Sort...");
        // Implement Merge Sort logic
    }
}
```

### ✅ **Sorting Context**
```java
class Sorter {
    private SortingStrategy strategy;

    public void setSortingStrategy(SortingStrategy strategy) {
        this.strategy = strategy;
    }

    public void sort(int[] numbers) {
        if (strategy == null) {
            throw new IllegalStateException("Sorting strategy not set!");
        }
        strategy.sort(numbers);
    }
}
```

### ✅ **Client Code**
```java
public class StrategyPatternSorting {
    public static void main(String[] args) {
        Sorter sorter = new Sorter();

        // Use Bubble Sort
        sorter.setSortingStrategy(new BubbleSort());
        sorter.sort(new int[]{5, 2, 9, 1});

        // Switch to Quick Sort
        sorter.setSortingStrategy(new QuickSort());
        sorter.sort(new int[]{8, 3, 7, 4});

        // Switch to Merge Sort
        sorter.setSortingStrategy(new MergeSort());
        sorter.sort(new int[]{6, 1, 5, 9});
    }
}
```

### **🔹 Output**
```
Sorting using Bubble Sort...
Sorting using Quick Sort...
Sorting using Merge Sort...
```

---

## 🌍 7. Real-World Applications  
✔ **Payment Processing Systems** – Users can select different payment methods dynamically.  
✔ **Sorting Algorithms** – Selecting different sorting methods dynamically.  
✔ **Compression Algorithms** – Choosing between ZIP, RAR, GZIP at runtime.  
✔ **Navigation Systems** – Selecting different routes (Shortest Path, Scenic Route, etc.).  

---

## 🔥 8. Advantages & Disadvantages  
### ✅ **Advantages**  
✔ **Promotes Open-Closed Principle** – Easily add new strategies without modifying existing code.  
✔ **Reduces complex if-else conditions** by separating logic into individual classes.  
✔ **Increases code flexibility** by allowing dynamic behavior changes.  

### ❌ **Disadvantages**  
✘ **Increases number of classes**, leading to slightly more complex code.  
✘ **Requires careful strategy selection** to avoid unnecessary complexity.  

---

## 🎯 9. Conclusion  
The **Strategy Pattern** is useful when you need to define multiple **interchangeable algorithms** and allow them to be selected dynamically at runtime. It **improves code maintainability and scalability**. 🚀
