# -Nutrition-Aware-Recipe-Recommendation-
# Cyber-Intrusion Detection KB: Hybrid Architecture

This project implements a **Hybrid AI Architecture** for cyber-intrusion detection, specifically designed for a Knowledge Representation and Reasoning course. It integrates the predictive power of **Deep Learning (DL)** with the logical rigor of **Knowledge Representation (KR)** to provide high-level, explainable alerts based on temporal attack sequences.

---

### **Project Overview**

The system processes low-level network anomalies identified by a DL model and subjects them to a **semantic reasoning pipeline**. By evaluating these anomalies against a set of **Horn Clauses** stored in a Knowledge Base (KB), the system can distinguish between isolated incidents and sophisticated, multi-stage attack patterns.

* **Logic Engine**: Datalog (via `pyDatalog`).
* **Knowledge Base**: OWL/RDF Ontology (via `owlready2`).
* **Reasoning Type**: Temporal Reasoning (Sequencing over time).
* **Environment**: Google Colab.

---

### **System Architecture**

The integration consists of three distinct phases:

1. **Anomaly Detection (DL Layer)**: A Deep Learning model monitors network traffic and outputs timestamped flags (e.g., "PortScan," "FailedLogin") when suspicious activity is detected.
2. **Semantic Mapping (Integration Layer)**: These discrete flags are injected into the Datalog engine as logical facts.
3. **Temporal Reasoning (KR Layer)**: The system checks these facts against predefined attack signatures. For example, it validates if a `PortScan` was followed by a `FailedLogin` and a `SudoAttempt` in a specific chronological order.

---

### **Installation & Setup**

To run this project in **Google Colab**, install the necessary dependencies:

```python
!pip install owlready2 pyDatalog

```

### **Core Logic: The Horn Clause**

The system identifies high-level threats using the following logic:

* **Rule**: `AlertLevel('High') <= Anomaly('PortScan', T1) & Anomaly('FailedLogin', T2) & Anomaly('SudoAttempt', T3) & (T1 < T2) & (T2 < T3)`

This ensures an alert is only triggered if the events occur in the correct sequence over time.

---

### **Usage**

1. **Upload Ontology**: Upload your `my.txt` (OWL/XML) file to the Colab environment.
2. **Clean & Load**: The script programmatically removes broken internal imports (such as `urn:webprotege` references) and re-saves the file as a valid `.rdf` resource.
3. **Execute**: Run the reasoning cell to process the DL output stream and generate alert levels.

---

### **Key Features**

* **Transitive Reasoning**: Deduces high-level security statuses from low-level data hierarchies.
* **Error Resiliency**: Includes logic to reset the Datalog engine state to prevent `NoneType` errors during iterative development in notebooks.
* **Explainable AI**: Unlike "black-box" models, this system provides a clear logical trace for why a "High" alert level was triggered.
