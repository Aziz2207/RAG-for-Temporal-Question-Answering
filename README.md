![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![LLaMA](https://img.shields.io/badge/LLaMA--3-Foundation_Model-orange?style=for-the-badge)
![RAG](https://img.shields.io/badge/RAG-Retrieval--Augmented--Generation-blue?style=for-the-badge)
![NLP](https://img.shields.io/badge/NLP-Temporal_QA-purple?style=for-the-badge)

# 🧠 RAG for Temporal Question Answering
### INF8460 — Natural Language Processing (Academic Project)

This repository contains the implementation and report for **TP4 of the INF8460 course** at **Polytechnique Montréal**.

The project focuses on **Temporal Question Answering (Temporal QA)** using a **Retrieval-Augmented Generation (RAG)** approach built on top of a **large language model (LLaMA-3.2-3B-Instruct)**.

---

## 🎯 Project Objectives

- Build a **temporal question answering system**
- Combine **parametric knowledge** (LLM) with **external factual knowledge**
- Implement a **RAG pipeline** for factual grounding
- Design **robust evaluation metrics** for QA
- Explore **prompt engineering** and **few-shot learning**
- Compete in a **Kaggle-style academic competition**

---

## 📂 Dataset & Task

### Task
Given a natural language question, the model must output the **correct temporal or factual answer**.

**Example:**


### Dataset Characteristics
- Public dataset based on **Wikipedia / Wikidata**
- Question types:
  - `Explicit`
  - `Temp.Ans`
  - `Ordinal`
  - `Implicit`
- Splits:
  - Train: 6,970 questions
  - Validation: 3,236 questions
  - Test: 3,237 questions
- ~240,000 structured factual triples used for retrieval

Each question is associated with:
- entities (Wikidata QIDs)
- temporal information
- gold answers (IDs and natural language)
- neighborhood facts for retrieval

---

## 🏗️ System Architecture

### Base Model
- **LLaMA-3.2-3B-Instruct**
- Loaded with **4-bit quantization (BitsAndBytes)** for memory efficiency
- Used in **decoder-only autoregressive generation**

### Pipeline Overview
1. **Prompt construction**
2. **Optional few-shot examples**
3. **LLM generation**
4. **(RAG) Retrieval of relevant facts**
5. **Answer generation**
6. **Evaluation (Exact / Partial Match)**

---

## 🔎 Retrieval-Augmented Generation (RAG)

The RAG approach enhances the LLM by:
- retrieving relevant factual triples from a large knowledge base
- injecting them into the prompt context
- reducing hallucinations
- improving factual accuracy for temporal reasoning

This allows the model to answer questions **beyond its parametric memory**.

---

## ✍️ Prompt Engineering

Multiple prompting strategies were implemented:
- **Natural Language answers**
- **Wikidata entity ID answers**
- Strict output formatting constraints
- System prompts to reduce verbosity and hallucinations

A custom `PromptManager` class handles:
- zero-shot prompts
- few-shot prompts
- dynamic prompt construction

---

## 🧪 Few-Shot Learning

Few-shot prompting was evaluated by injecting:
- 5 randomly selected QA examples from the training set

**Observed effects:**
- Improved answer formatting
- Better adherence to constraints
- Increased recall and F1-score on validation data

---

## 📊 Evaluation Metrics

A custom evaluation module was implemented:

### Exact Match (EM)
- Prediction must exactly match the reference answer

### Partial Match (PM)
- At least one overlapping word between prediction and reference

Metrics computed:
- Precision
- Recall
- F1-score (per question and averaged)

This evaluation setup closely reflects **real-world QA constraints**.

---

## 📈 Key Results & Observations

- LLMs perform better in **natural language output** than strict entity IDs
- Prompt design has a **major impact** on performance
- Few-shot prompting significantly improves results
- RAG reduces hallucinations in temporal reasoning tasks
- Exact Match remains challenging for structured answers

---

## 👥 Team & Contributions

**Team:**
- Aziz Hidri  
- Amaury Miquel  
- Bazoune Mahdi Fares  

Each member independently explored solutions; the final implementation combines the **best-performing approaches**.

---

## 🎓 Academic Context & Integrity

- Course: **INF8460 – Traitement automatique de la langue naturelle**
- Semester: **Fall 2025**
- Institution: **Polytechnique Montréal**
- Academic competition component included
- **Use of generative AI tools was strictly prohibited**

---

## ⚠️ Disclaimer

This project is for **educational and research purposes only**.  
It is not intended for production or commercial deployment.

