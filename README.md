# 📝 Document Editor Application (LLD)

A Low-Level Design (LLD) of a scalable **Document Editor Application** (similar to Google Docs) using a **bottom-up approach**, **UML diagrams**, and adhering to the **SOLID design principles**.

---

## SOLID Design Principles 

1. **S - Single Responsibility Principle (SRP)** : A class should have only one reason to change, meaning it should have only one responsibility or function.

2. **O - Open/Closed Principle (OCP)** : Entities (classes, modules, functions) should be open for extension but closed for modification - you should be able to add new features without changing existing code.

3. **L - Liskov Subtitution Principle (LSP)** : Subtypes must be substitutable for their base types. That means a derived class should extend the base class without changing its behaviour.

4. **I - Interface Segregation Principle (ISP)** : Client should not be forced to depend on interfaces they do not use.

5. **D - Dependency Inversion Principle (DIP)** : High-level modules should not depend on low-level modules. Both should depend on abstraction. Also, Abstractions should not depend on details; details should depend on abstractions.

## 📌 Problem Statement

Design a Document Editor Application that supports:
- Adding **text**, **images**, **new lines**, and **tabs**
- Rendering the final document
- Saving it to **file** or **database**
- Seamless **scalability** for new features
- Clean, modular design following **SOLID principles**

---

## ⚙️ Initial Design (Problematic)

```cpp
class DocumentEditor {
    vector<String> elements;

    void addText(String text);
    void addImage(String path);
    void renderDocument(); // Business Logic
    void saveToFile();     // Business Logic
};
```

### Problems:
- ❌ Violates SRP – handles multiple responsibilities

- ❌ Violates OCP – hard to extend for new features

- ❌ No LSP, ISP, DIP usage

## ✅ Final Solution (SOLID Applied)

## **Polymorphism for Document Elements**

```cpp
abstract class DocumentElement {
    void render();
};

class TextElement : DocumentElement { void render(); };
class ImageElement : DocumentElement { void render(); };
class NewLineElement : DocumentElement { void render(); };
class TabSpaceElement : DocumentElement { void render(); };
```

## **Document Class (Handles Element Collection**

```cpp
class Document {
    vector<DocumentElement> elements;

    void addElement(DocumentElement el);
    vector<DocumentElement> getElements();
};
```

## **Persistence Abstraction**

```cpp
abstract class Persistence {
    void save(String data);
};

class SaveToFile : Persistence { void save(String data); };
class SaveToDB : Persistence { void save(String data); };
```

## **DocumentEditor Class**

```cpp
class DocumentEditor {
    Document doc;
    Persistence storage;

    void addText(String text);
    void addImg(String path);
    void addNewLine();
    void addTabSpace();
    void save();
};
```

## **Renderer Separated (SRP Improvement)**

```cpp
class DocumentRenderer {
    Document doc;

    void render();
};
```

## ✅ SOLID Principle Mapping

1. SRP
- Description : Each class has one responsibility
- Applied In : Document, Persistence, Renderer, Editor

2. OCP
- Description : Extend without modifying base
- Applied In : New DocumentElement or Persistence types

3. LSP
- Description : Subtypes can replace base types
- Applied In : TextElement, ImageFormat via DocumentElement

4. ISP
- Description : Interface contains only what's necessary
- Applied In : render() in DocumentElement, save() in Persistence

5. DIP
- Description : Depend on Abstractions
- Applied In : DocumentEditor depends on Persistence, not concrete class

## 📷 UML Diagrams

![1](https://github.com/user-attachments/assets/cf0ae54a-4c6b-4cb9-a462-74dcc4685ce5)

## 🔧 Further Design Improvements

**Extracting Rendering Logic from Document**

To maintain Single Responsibility, the render() method is extracted from the Document class and placed in a new DocumentRenderer class.

This ensures that:
- Document remains focused only on storing and managing document elements.
- DocumentRenderer is solely responsible for rendering logic.

## 📷 UML Diagram after Improvement

![2](https://github.com/user-attachments/assets/36b19a66-1037-4b62-a0e8-8aed0fff7abc)


## 📘 Note
No LLD is perfect. There is always room for iterative improvement, whether in abstraction, decoupling, or scaling design patterns.

## 👨‍💻 Author
Anirudh Chaudhary
Passionate about system design and clean code architecture.
