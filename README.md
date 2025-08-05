# IntegrationProject calculator

This integration project was developed during my internship at **Saib IT**, focusing on data flow between multiple applications, file processing, and service-based architecture using SOAP and HTTP protocols.

The system is composed of **three main applications** that work together to process mathematical operations through a UI, transform data using DFDL, expose services via SOAP, and validate results using a JSON schema.

---

## ⚙️ Overview of Applications

### 1. **JavaFX UI**
- Accepts user input for mathematical operations.
- Automatically writes the input to a local text file in a **predefined structured format**.

### 2. **FileReader Application**
- Reads the formatted text file using a **DFDL schema**.
- Internally triggers the **Web Calculator Service** (SOAP-based), which performs the actual calculations.
- The **Web Calculator Service** exposes a WSDL and can be tested using **SOAP UI** or used in other application(like in our case).
- After calculations, the FileReader application writes the results into a new text file in **JSON format**.

### 3. **Operator Aggregator Application**
- Reads the output JSON file from the previous step.
- Validates the structure and content using a **JSON Schema**.
- Counts the number of operations executed per operator (e.g., `+`, `-`, `*`, `/`).
- This application is triggered via **GET** using **Postman**.

---

## 🔄 Data Flow

```plaintext
JavaFX UI (User Input)
        ↓
Formatted Text File (Saved Automatically)
        ↓
FileReader App
  ├─> Reads file using DFDL
  ├─> Invokes Web Calculator (SOAP, WSDL)
  └─> Writes JSON output
        ↓
Operator Aggregator App
  ├─> Validates with JSON Schema
  └─> Counts operations
