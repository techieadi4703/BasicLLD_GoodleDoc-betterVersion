# Document Editor - Improved C++ Version

## Overview
This project demonstrates an enhanced Document Editor implemented in C++ that leverages object-oriented programming principles such as abstraction, inheritance, and polymorphism. The editor allows you to add different types of elements (text, images, new lines, tabs) into a document, render the document as a formatted string, and save it persistently to a file.

---

## Features
- **Extensible document elements:** Supports text, images, new lines, and tab spaces, each implemented as separate classes inheriting from an abstract base class `DocumentElement`.
- **Flexible rendering:** Each element renders itself in a customized way (e.g., text wrapped in `[Text: ...]`, images wrapped in `[Image: ...]`).
- **Persistence abstraction:** The document can be saved through various storage mechanisms. Currently supports saving to a file, with a placeholder for database storage.
- **Separation of concerns:** The `DocumentEditor` class manages user interactions, the `Document` class manages element storage, and the `Persistence` interface manages saving data.

---

## LLD Design Principles

This project follows key Low-Level Design (LLD) principles to ensure clean, maintainable, and extensible code:

- **Abstraction:** Abstract base classes like `DocumentElement` and `Persistence` separate interface from implementation.
- **Encapsulation:** Data and behavior are bundled within classes like `TextElement`, `ImageElement`, and `Document`.
- **Polymorphism:** Different document elements override the `render()` method for customized behavior.
- **Separation of Concerns:** Document management, rendering, and persistence are handled by distinct classes (`Document`, `DocumentEditor`, and `Persistence`).
- **Extensibility:** New document elements or storage mechanisms can be added with minimal changes to existing code.

These principles collectively contribute to a modular and scalable design.

---

## Code Structure

### Classes
- **DocumentElement (abstract)**  
  Base class for all document elements. Declares a pure virtual method `render()`.

- **TextElement**  
  Represents a block of text in the document.

- **ImageElement**  
  Represents an image reference in the document.

- **NewLineElement**  
  Represents a newline (line break).

- **TabSpaceElement**  
  Represents a tab space.

- **Document**  
  Holds a collection of `DocumentElement` pointers and concatenates their rendered output.

- **Persistence (abstract)**  
  Interface for saving document data.

- **FileStorage**  
  Implements `Persistence` by saving document content to a file (`betterVersion.txt`).

- **DBStorage** (Placeholder)  
  Intended for future database persistence implementation.

- **DocumentEditor**  
  User-facing class managing document construction, rendering, and persistence.

---

## Usage Example

```cpp
Document* document = new Document();
Persistence* persistence = new FileStorage();

DocumentEditor* editor = new DocumentEditor(document, persistence);

editor->addText("Hello, world!");
editor->addNewLine();
editor->addText("This is a real-world document editor example.");
editor->addNewLine();
editor->addTabSpace();
editor->addText("Indented text after a tab space.");
editor->addNewLine();
editor->addImage("picture.jpg");

cout << editor->renderDocument() << endl;
editor->saveDocument();


### 🖥️ Sample Output
[Text: Hello, world!]
[Text: This is a real-world document editor example.]
    [Text: Indented text after a tab space.]
[Image: picture.jpg]


## 📂 File Generated
- `betterVersion.txt`: Contains the rendered output

## 📦 Compilation & Execution
To compile and run the program:

```bash
g++ -o editor main.cpp
./editor
