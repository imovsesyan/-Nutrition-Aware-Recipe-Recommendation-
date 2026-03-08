# Nutrition-Aware Recipe Recommendation System

### Hybrid AI + Knowledge Representation Approach

**Course:** Artificial Intelligence / Knowledge Representation
**Project:** Nutrition-Aware Recipe Recommendation KB Design
**Team Members:**

* Inesa Movsisyan
* *(add teammates if you have)*

---

# Project Overview

This project presents a **hybrid Artificial Intelligence system** that combines **Deep Learning (DL)** with **Knowledge Representation (KR)** to recommend recipes while respecting dietary restrictions.

Traditional recommendation systems rely purely on machine learning models, which operate as **black-box predictors** and do not guarantee dietary safety. To address this limitation, our system integrates a **semantic knowledge base (ontology)** that enables logical reasoning about ingredients and allergens.

The system works in two stages:

1. **Deep Learning model** generates a ranked list of recipe recommendations.
2. **Knowledge Representation component (ontology reasoning)** verifies that the recommended recipes satisfy dietary constraints.

For example:

If a recipe contains **Soy Sauce**, and the ontology defines:

```
Soy Sauce → containsAllergen → Gluten
```

the reasoner automatically deduces:

```
Recipe → NotGlutenFreeRecipe
```

and the system filters the recipe if the user requires **gluten-free food**.

---

# System Architecture

The architecture consists of three main components:

1. **Recipe Recommendation Model**
2. **Ontology-based Knowledge Base**
3. **Reasoning Engine**

```
User Preferences
       ↓
Deep Learning Model
       ↓
Candidate Recipes
       ↓
Knowledge Base Reasoning
       ↓
Filtered Safe Recipes
```

---

# Knowledge Base Design

The knowledge base was implemented using **OWL ontology** and designed in **Protégé / WebProtégé**.

### Core Concepts

**Classes**

* Recipe
* Ingredient
* Allergen
* Gluten
* Nuts

**Ingredient Categories**

* GlutenIngredient
* NutIngredient

**Defined Recipe Classes**

* NotGlutenFreeRecipe
* ContainsNutsRecipe

---

### Object Properties

| Property      | Domain     | Range      | Description                  |
| ------------- | ---------- | ---------- | ---------------------------- |
| hasIngredient | Recipe     | Ingredient | Links recipes to ingredients |
| hasAllergen   | Ingredient | Allergen   | Defines allergen content     |

---

### Logical Reasoning Rules

The ontology uses **Description Logic** reasoning.

Example rule:

```
NotGlutenFreeRecipe ≡
Recipe AND (hasIngredient some (hasAllergen some Gluten))
```

This means:

Any recipe containing an ingredient that contains gluten
→ automatically becomes **NotGlutenFreeRecipe**.

---

# Example Reasoning

### Ingredient Knowledge

```
Soy Sauce ⊑ hasAllergen some Gluten
WheatFlour ⊑ hasAllergen some Gluten
Almond ⊑ hasAllergen some Nuts
```

### Recipes

```
ramen1
   hasIngredient soy1
   hasIngredient flour1

salad1
   hasIngredient almond1
```

### Reasoner Output

```
ramen1 → NotGlutenFreeRecipe
salad1 → ContainsNutsRecipe
```

---

# Repository Structure

```
project-root
│
├── README.md
│
├── src/
│   ├── model.py
│   ├── training.py
│   ├── inference.py
│   └── reasoning.py
│
├── data/
│   └── sample_recipes.csv
│
├── models/
│   └── trained_model_checkpoint.pt
│
├── kb/
│   ├── recipe_ontology.owl
│   └── recipe_ontology.omn
│
└── requirements.txt
```

---

# Setup Instructions

### 1 Install Python Environment

Recommended Python version:

```
Python 3.9+
```

Create a virtual environment:

```bash
python -m venv venv
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# Dependencies

Main libraries used:

* Python
* PyTorch / TensorFlow
* OWL API
* rdflib
* numpy
* pandas
* scikit-learn

---

# Running the Project

### Train the Model

```bash
python src/training.py
```

This trains the recipe recommendation model and saves the weights in:

```
models/
```

---

### Run Inference

```bash
python src/inference.py
```

This generates a ranked list of recipe recommendations.

---

### Run Knowledge Base Reasoning

```bash
python src/reasoning.py
```

This step loads the ontology and filters recipes violating dietary constraints.

---

# Ontology Reasoning

The ontology was developed using:

* **Protégé Desktop**
* **WebProtégé**

Reasoning engines used:

* **HermiT**
* **ELK**

Reasoning verifies that recipes satisfy dietary requirements such as:

* Gluten-free
* Nut-free
* Vegan
* Allergen-free

---

# Results

The hybrid architecture successfully demonstrates that **semantic reasoning can improve recommendation safety**.

Key results:

* Recipes containing gluten ingredients were automatically classified as **NotGlutenFreeRecipe**.
* Recipes containing nuts were classified as **ContainsNutsRecipe**.
* The reasoning layer effectively filtered unsafe recommendations.

This approach improves **interpretability, reliability, and dietary safety** compared to traditional black-box recommender systems.

---

# Future Work

Possible improvements include:

* Expanding the ontology using **FoodOn**
* Adding more allergens
* Integrating nutritional constraints (calories, protein, fat)
* Implementing real-time recommendation filtering
* Using Graph Neural Networks for recipe embeddings

---

# Tools Used

* Protégé Desktop
* WebProtégé
* Python
* OWL Ontology
* Description Logic Reasoning
* HermiT Reasoner

---

# License

This project is developed for academic purposes as part of the Artificial Intelligence course.


Just tell me.
