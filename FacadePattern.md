# **Facade Design Pattern**

## **1. Definition**
The **Facade Pattern** is a **structural design pattern** that provides a **simplified interface** to a larger and more complex system. It hides the complexities of the underlying system by exposing a unified, easy-to-use interface for clients.

---

## **2. Key Concepts**
- Acts as a **wrapper** around a set of subsystems to provide a simple API.
- Reduces **dependencies** between client code and complex subsystems.
- Helps in improving **code maintainability and readability**.

---

## **3. Key Components**
1. **Facade** – The high-level interface that simplifies interactions with subsystems.
2. **Subsystems** – The underlying complex classes that perform various functionalities.
3. **Client** – Uses the Facade to interact with the system without dealing with complexities.

---

## **4. When to Use Facade Pattern?**
- When a system is **too complex** and you want to provide a **simplified interface**.
- When you need to **decouple clients** from intricate subsystem details.
- When you want to **improve maintainability** by reducing dependencies.
- When working with **legacy systems** where a cleaner interface is required.

---

## **5. Example in Java**
### **Scenario:**
A **Home Theater System** has multiple components like an **Amplifier, DVD Player, Projector, and Speakers**. Instead of making the client interact with all these components separately, we create a **Facade** that provides a simple `watchMovie()` method.

```java
// Step 1: Subsystem Components
class Amplifier {
    public void on() { System.out.println("Amplifier turned ON"); }
    public void setVolume(int level) { System.out.println("Amplifier volume set to " + level); }
}

class DVDPlayer {
    public void on() { System.out.println("DVD Player turned ON"); }
    public void play(String movie) { System.out.println("Playing movie: " + movie); }
}

class Projector {
    public void on() { System.out.println("Projector turned ON"); }
    public void setInput(String source) { System.out.println("Projector input set to " + source); }
}

class Speakers {
    public void on() { System.out.println("Speakers turned ON"); }
    public void setSurroundSound() { System.out.println("Surround Sound enabled"); }
}

// Step 2: Facade Class
class HomeTheaterFacade {
    private Amplifier amp;
    private DVDPlayer dvd;
    private Projector projector;
    private Speakers speakers;

    public HomeTheaterFacade(Amplifier amp, DVDPlayer dvd, Projector projector, Speakers speakers) {
        this.amp = amp;
        this.dvd = dvd;
        this.projector = projector;
        this.speakers = speakers;
    }

    public void watchMovie(String movie) {
        System.out.println("Setting up home theater...");
        amp.on();
        amp.setVolume(5);
        dvd.on();
        dvd.play(movie);
        projector.on();
        projector.setInput("DVD");
        speakers.on();
        speakers.setSurroundSound();
        System.out.println("Enjoy your movie!");
    }
}

// Step 3: Client Code
public class FacadePatternExample {
    public static void main(String[] args) {
        Amplifier amp = new Amplifier();
        DVDPlayer dvd = new DVDPlayer();
        Projector projector = new Projector();
        Speakers speakers = new Speakers();

        HomeTheaterFacade homeTheater = new HomeTheaterFacade(amp, dvd, projector, speakers);
        homeTheater.watchMovie("Inception");
    }
}
```

---

## **6. Output**
```
Setting up home theater...
Amplifier turned ON
Amplifier volume set to 5
DVD Player turned ON
Playing movie: Inception
Projector turned ON
Projector input set to DVD
Speakers turned ON
Surround Sound enabled
Enjoy your movie!
```
The **Facade** hides the complexity of setting up the home theater and provides a single method `watchMovie()` to handle everything.

---

## **7. Real-World Examples**
- **Spring Framework’s JdbcTemplate** – Simplifies database interactions.
- **Operating Systems** – Provides a unified API to manage files, devices, and processes.
- **Payment Gateways** – Exposes a single API while handling various banking systems internally.

---

## **8. Advantages & Disadvantages**
### ✅ **Advantages**
- **Simplifies complex systems** by providing a high-level interface.
- **Reduces dependencies** between clients and subsystems.
- **Improves maintainability** by decoupling different parts of the system.

### ❌ **Disadvantages**
- **Overuse** can lead to a **god object** that holds too much responsibility.
- **Limited flexibility** if new functionalities need to be exposed from subsystems.

---

## **9. Conclusion**
The **Facade Pattern** is useful when dealing with **complex systems** by providing a **clean and simple interface**. It helps in **decoupling** subsystems from clients, making the system more maintainable and easy to use. 🚀
