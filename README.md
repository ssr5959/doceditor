# Document Editor – C++ (Low-Level Design)

##  Overview

This project demonstrates a simple document editor that supports adding **text**, **images**, **tabs**, and **new lines** to a document and saving it to a file.

The original implementation followed a poor design with minimal structure, mixing logic and data types in a single class. This was later refactored to follow **Object-Oriented Programming (OOP)** and **SOLID principles**, significantly improving code quality, scalability, and maintainability.

---

##  Original (Bad) Design

The initial implementation included:

- A single `DocumentEditor` class that handled:
  - Adding both text and images as raw `string`s
  - Rendering logic based on manual string-type checks (e.g., checking `.jpg` extension)
  - File I/O operations
- **Tightly coupled** logic and **poor separation of concerns**
- No abstraction or extensibility for other document components (e.g., newlines, tabs, etc.)
- Violation of **Open-Closed Principle** (code needed modification for adding new element types)

---

##  Refactored (Good) Design – SOLID Principles Applied

The improved version introduces a **Low-Level Design (LLD)** with the following structure:

### 1. **Single Responsibility Principle (SRP)**
Each class has a well-defined responsibility:
- `TextElement`, `ImageElement`, `NewLineElement`, `TabSpaceElement`: handle rendering logic for each document element.
- `Document`: stores and renders all elements.
- `DocumentEditor`: acts as a client-facing facade.
- `Persistence` interface: abstract layer for storage.
- `FileStorage`: handles saving documents to file.

### 2. **Open-Closed Principle (OCP)**
- You can add new types of document elements (e.g., audio, tables) without changing existing code.
- Just create a new subclass of `DocumentElement` and implement `render()`.

### 3. **Liskov Substitution Principle (LSP)**
- All subclasses of `DocumentElement` can be used wherever a `DocumentElement*` is expected.
  
### 4. **Interface Segregation Principle (ISP)**
- Separate `Persistence` interface ensures storage responsibility is decoupled from document generation.

### 5. **Dependency Inversion Principle (DIP)**
- `DocumentEditor` depends on abstraction (`Persistence`) rather than a concrete file-saving class.
- You can switch to database storage (via `DBStorage`) without changing the editor logic.

---

## 🔧 Technologies Used
- C++ (OOP + LLD)
- Standard Library (`<fstream>`, `<vector>`, `<string>`)

---

## How to Run

1. **Compile the project:**
   ```bash
   g++ -o document_editor main.cpp
