# 🧮 IntegrationProject Calculator

This integration project was developed during my internship at **Saib IT**, focusing on orchestrating data flow between multiple applications, structured file processing, and service-based architecture using **IBM App Connect Enterprise (ACE)**. It demonstrates how to build and integrate **SOAP services**, **DFDL parsers**, **JSON schema validators**, and **REST APIs** to automate mathematical operations across a modular system.

---

## ⚙️ Overview of Applications

### 1. JavaFX UI (External)
- Built using JavaFX to collect user input for mathematical expressions (e.g., `8 * 4`).
- Automatically saves input to a **local structured text file**.
- ⚠️ **Note**: The file path must be manually updated in the Java code based on your environment.

---

### 2. FileReader Application (IBM ACE)
- Reads the structured input file.
- Parses the content using a **DFDL schema** (imported from a shared library).
- Triggers the internal **Web Calculator Service** using a **SOAPRequest** node and WSDL.
- Writes the result into a **JSON-formatted output file**.

---

### 3. Web Calculator Service (IBM ACE)
- A custom SOAP web service built in IBM ACE.
- Uses **SOAPInput**, **Compute**, and **SOAPReply** nodes.
- Performs the requested arithmetic operation and returns the result.
- Exposes a **WSDL endpoint**, which can be tested using **SOAP UI** or called by other ACE applications (like FileReader).

---

### 4. Operator Aggregator Application (IBM ACE)
- Reads the output JSON file created by the FileReader.
- Validates it using a **JSON Schema** (from a shared library).
- Counts how many times each operator was used (`+`, `-`, `*`, `/`).
- Exposes a **RESTful GET endpoint**, testable using **Postman**.

---

## 🔄 Data Flow

```plaintext
JavaFX UI (User Input)
        ↓
Structured Text File (Saved Locally)
        ↓
FileReader App (IBM ACE)
  ├─> Parses input using DFDL
  ├─> Calls Web Calculator Service (SOAP, internal ACE app)
  └─> Writes result as JSON file
        ↓
Operator Aggregator App (IBM ACE)
  ├─> Validates JSON using Schema
  └─> Counts operations and returns summary via REST GET
