# -Nutrition-Aware-Recipe-Recommendation-
# Nutrition-Aware Recipe Recommendation System

This project implements a **Hybrid AI Architecture** that combines the predictive capabilities of **Deep Learning (DL)** with the logical constraints of **Knowledge Representation (KR)** to provide personalized, safety-conscious food recommendations.

---

### **Project Overview**

The system is designed to bridge the gap between "black-box" recommendation models and the strict requirements of dietary safety. While a DL model predicts what a user might enjoy, a **semantic reasoning pipeline** ensures the recommendation adheres to specific dietary logic, such as veganism or allergen avoidance.

* **Primary Ontology**: Utilizing **FoodOn** for ingredient classification.
* **Reasoning Engine**: **HermiT** reasoner for transitive and logical deduction.
* **Logic Framework**: **Description Logic (DL)** axioms for ingredient and recipe classification.

---

### **System Architecture**

The project is developed in three distinct phases:

1. **Taxonomy Phase**: Establishing the ingredient hierarchy and properties (e.g., origin, allergen content) using the FoodOn ontology.
2. **Logic Phase**: Implementing formal logic axioms. For example, using **universal quantification** ($\forall$) to define a "Vegan Recipe" as one that consists *only* of plant-based ingredients.
3. **Integration Phase**: Filtering DL recommendation outputs through the reasoning pipeline to ensure compliance with the user's health or ethical constraints.

---

### **Core Functionality**

* **Dietary Classification**: Automatically determines if a recipe is Vegan, Vegetarian, or Gluten-Free based on its ingredient list.
* **Allergen Detection**: Uses transitive reasoning to deduce "Not Gluten-Free" if a recipe contains an ingredient derived from wheat, even if not explicitly labeled.
* **Safety-First Recommendations**: Deep Learning outputs are cross-referenced with the Knowledge Base; if a recommendation violates a logical constraint, it is discarded or flagged.

---

### **Technologies Used**

* **Python**: Core development language.
* **Owlready2**: For loading and manipulating ontologies.
* **HermiT**: For executing complex semantic reasoning.
* **Knowledge Representation & Reasoning (KRR)**: The theoretical foundation of the system.

---

### **Development Status**

The project is currently in the final reporting stage, with the three phases of development (Taxonomy, Logic, and Integration) successfully implemented and tested for logical rigor.
