## **Composite Design Pattern**

### **1. Definition**
The **Composite Pattern** is a **structural design pattern** used to treat **individual objects** and **compositions of objects** **uniformly**. It allows clients to interact with **both single objects and groups of objects in the same way**, making it easier to work with hierarchical structures (like trees).

---

### **2. Key Concepts**
- It organizes objects into **tree structures**.
- Allows **clients to treat both individual objects and compositions uniformly**.
- Used when **part-whole hierarchies** need to be represented.

---

### **3. Key Components**
1. **Component (Abstract Class / Interface)** – Declares operations for both simple and complex elements.
2. **Leaf (Concrete Class)** – Represents individual objects in the hierarchy.
3. **Composite (Concrete Class)** – Represents a container that holds child components.
4. **Client** – Uses the component interface to work with objects uniformly.

---

### **4. When to Use Composite Pattern?**
✔ When objects need to be represented as **hierarchical structures** (e.g., trees).  
✔ When you want to **treat individual objects and groups uniformly**.  
✔ When **a recursive structure** is needed (e.g., directories, organization hierarchies).  
✔ When operations should **apply to both single objects and groups** without differentiating.  

---

### **5. Example in Java**
#### **Scenario:**  
We are modeling a file system where **files** and **folders** both implement the same interface, allowing us to interact with them uniformly.

```java
// Step 1: Define the Component Interface
interface FileSystem {
    void showDetails();
}

// Step 2: Create the Leaf Class (Single Object - File)
class File implements FileSystem {
    private String name;

    public File(String name) {
        this.name = name;
    }

    @Override
    public void showDetails() {
        System.out.println("File: " + name);
    }
}

// Step 3: Create the Composite Class (Container - Folder)
import java.util.ArrayList;
import java.util.List;

class Folder implements FileSystem {
    private String name;
    private List<FileSystem> children = new ArrayList<>();

    public Folder(String name) {
        this.name = name;
    }

    public void add(FileSystem component) {
        children.add(component);
    }

    @Override
    public void showDetails() {
        System.out.println("Folder: " + name);
        for (FileSystem child : children) {
            child.showDetails();
        }
    }
}

// Step 4: Client Code
public class CompositePatternExample {
    public static void main(String[] args) {
        FileSystem file1 = new File("file1.txt");
        FileSystem file2 = new File("file2.txt");

        Folder folder1 = new Folder("My Documents");
        folder1.add(file1);
        folder1.add(file2);

        Folder rootFolder = new Folder("Root");
        rootFolder.add(folder1);
        rootFolder.add(new File("file3.txt"));

        rootFolder.showDetails();
    }
}
```

---

### **6. Output**
```
Folder: Root
Folder: My Documents
File: file1.txt
File: file2.txt
File: file3.txt
```
This shows how **both individual files and folders** are handled in the same way.

---

### **7. Real-World Examples**
✔ **GUI Hierarchy** – Buttons, Panels, and Windows in UI libraries.  
✔ **File System** – Folders containing files and other folders.  
✔ **Organization Structure** – Employees, Managers, and Departments.  
✔ **XML/HTML Document Structure** – Elements containing nested elements.  

---

### **8. Advantages & Disadvantages**
#### ✅ **Advantages**
✔ Provides a **flexible and scalable** design for hierarchical data.  
✔ Simplifies **client code**, as it can treat individual and grouped objects the same way.  
✔ Supports **recursive structures** like trees and graphs.  

#### ❌ **Disadvantages**
✘ Can lead to **complex debugging** when working with deeply nested structures.  
✘ May increase **memory consumption** if not designed efficiently.  

---

### **9. Conclusion**
The **Composite Pattern** is useful when dealing with hierarchical structures, such as trees or nested objects, allowing **clients to handle individual elements and groups uniformly**. 🚀
