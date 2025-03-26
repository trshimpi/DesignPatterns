The **Observer Design Pattern** is a behavioral design pattern where an object (called the **Subject**) maintains a list of its dependents (**Observers**) and notifies them of any state changes, typically by calling one of their methods.

---

## **Observer Design Pattern - Behavioral Pattern**
### **Definition**:
- The **Observer Pattern** defines a **one-to-many dependency** between objects so that when one object changes state, all its dependents (observers) are notified and updated automatically.

### **Key Components**:
1. **Subject (Observable)**:
   - Maintains a list of observers.
   - Provides methods to attach, detach, and notify observers.
   - Changes its state and informs observers about the changes.

2. **Observer**:
   - Defines an interface to be updated when the subject changes.
   - Implements the update logic.

3. **Concrete Subject**:
   - Stores state and notifies observers when changes occur.

4. **Concrete Observer**:
   - Implements the observer interface and updates state based on subject notifications.

---

## **When to Use the Observer Pattern?**
- When you have a scenario where **one object changes** and **multiple objects need to be updated automatically**.
- When an object needs to notify other objects **without knowing** their concrete implementation.
- Used in scenarios such as **event handling systems, message queues, notifications, stock market updates**, etc.

---

## **Example in Java**
Here's a simple example where a **news agency** (subject) notifies subscribers (observers) whenever there is a new update.

```java
import java.util.ArrayList;
import java.util.List;

// Step 1: Create an Observer interface
interface Observer {
    void update(String news);
}

// Step 2: Create a Subject (Observable) interface
interface Subject {
    void registerObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}

// Step 3: Implement the Concrete Subject (News Agency)
class NewsAgency implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String latestNews;

    public void setNews(String news) {
        this.latestNews = news;
        notifyObservers();  // Notify all observers
    }

    @Override
    public void registerObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(latestNews);
        }
    }
}

// Step 4: Implement Concrete Observer (Subscribers)
class NewsSubscriber implements Observer {
    private String subscriberName;

    public NewsSubscriber(String name) {
        this.subscriberName = name;
    }

    @Override
    public void update(String news) {
        System.out.println(subscriberName + " received news update: " + news);
    }
}

// Step 5: Test the Observer Pattern
public class ObserverPatternExample {
    public static void main(String[] args) {
        NewsAgency agency = new NewsAgency();

        // Creating observers
        Observer subscriber1 = new NewsSubscriber("Alice");
        Observer subscriber2 = new NewsSubscriber("Bob");

        // Registering observers to the subject
        agency.registerObserver(subscriber1);
        agency.registerObserver(subscriber2);

        // Changing state in the subject
        agency.setNews("Breaking News: Observer Pattern Implemented!");

        // Removing an observer
        agency.removeObserver(subscriber1);

        // Updating news again
        agency.setNews("Latest Update: Design Patterns are Important!");
    }
}
```

---

## **Real-World Examples**
1. **Event Listeners in GUI Applications**:
   - In **Swing/AWT**, when you click a button, an event listener (observer) is notified.
  
2. **Stock Market Ticker**:
   - Investors (observers) get notified when stock prices change.

3. **Chat Applications (Pub-Sub Model)**:
   - Users subscribe to chat rooms, and they receive updates when someone posts a message.

4. **Notifications System**:
   - Email or SMS notifications are triggered when there is an update in a system.

---

## **Advantages of Observer Pattern**
✔ **Loosely Coupled** – Subject and Observer are **independent** of each other.  
✔ **Scalable** – We can **add/remove observers** dynamically.  
✔ **Automates Updates** – No need to manually update observers.  

## **Disadvantages of Observer Pattern**
✘ **Memory Leaks** – If observers are not removed properly, they may still exist in memory, leading to memory leaks.  
✘ **Unexpected Updates** – Observers may receive updates they were not expecting, causing unintended behavior.  

---

This pattern is commonly used in real-world applications where **event-driven programming** is needed. Let me know if you need more details or examples! 🚀
