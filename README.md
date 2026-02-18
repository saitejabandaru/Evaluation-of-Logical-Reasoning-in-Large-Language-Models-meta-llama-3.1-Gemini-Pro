# Evaluation of Logical Reasoning in Large Language Models

## 📌 Overview
This project evaluates and compares the logical reasoning capabilities of:

- LLaMA-3 (70B) – Open-source
- Gemini-1.5-Pro – Closed-source

using two reasoning benchmark datasets:

- LogiQA
- ARCT (Argument Reasoning Comprehension Task)

Beyond measuring final answer accuracy, we analyze how LLMs reason identifying failure patterns through a structured error taxonomy and building an automated LLM-based Auto Evaluator to classify reasoning errors step-by-step.

---

## Why This Project Matters
Most evaluations of LLMs on logical reasoning datasets measure only the correctness of the final answer.

This project goes further by:

- Breaking reasoning chains line-by-line
- Separating each step into premise and conclusion
- Identifying exactly where logical breakdown occurs
- Categorizing reasoning failures into structured error types
- Automating reasoning evaluation using a custom GPT framework

Instead of asking “Was the answer correct?”, we ask: “Where did the reasoning fail, and why?”

---

## 📊 Final Model Accuracy (Zero-Shot CoT Prompting)

We evaluated both models using **zero-shot Chain-of-Thought prompting** across datasets.


## Results

| Model              | LogiQA Accuracy | ARCT Accuracy |
|--------------------|-----------------|---------------|
| **LLaMA-3 (70B)**  | 31.34%          | 54.28%       |
| **Gemini-1.5-Pro** | 61.14%          | 85.14%       |


## Key Observations

- Gemini significantly outperformed LLaMA-3 on both reasoning benchmarks.
- However, answer accuracy alone does not explain *how* reasoning differs between models — motivating deeper analysis.

---

## 🧩 Manual Reasoning Chain Analysis

We manually analyzed reasoning chains and developed a structured taxonomy.

## Broad Categories

- **RR** – Right Premise, Right Conclusion  
- **RW** – Right Premise, Wrong Conclusion  
- **WR** – Wrong Premise, Right Conclusion  
- **WW** – Wrong Premise, Wrong Conclusion  
- **NC** – No Conclusion  


## Subcategories (Examples)

### Wrong Premise

- Error Propagation  
- Misinterpretation  

### Wrong Conclusion

- Insufficient Information  
- Wrong Assumption  
- Contradiction  
- Hallucination  
- Wrong Reasoning  
- Error Propagation  

## Example Annotated Reasoning Chains

Example annotated reasoning chains can be found in:

- 📄 `ARCT_Llama Reasoning Chains.pdf`
- 📄 `LogiQA_LLAMA_GEMINI_Reasoning Chains.pdf`

---
## 🤖 Custom GPT-Based Auto Evaluator

Using manually annotated reasoning chains, we built a **Custom GPT Auto Evaluator**.

# Important Clarification

> The manually annotated reasoning chains used to guide the Custom GPT were **different from the evaluation set used to compute accuracy**, ensuring no data leakage.

## Auto Evaluator

The Auto Evaluator:

- Splits reasoning chains into individual sentences  
- Identifies premise and conclusion per step  
- Assigns taxonomy labels (RR, RW, WR, WW, NC)  
- Applies subcategory classification  

Prompt design and taxonomy framework are documented in:

📄 `Custom_GPT_Autoevaluator_Instructions_.pdf`

## 📈 Auto Evaluator Performance

When compared against independently manually annotated reasoning chains:

- **Broad Category Accuracy:** 81.98%  
- **Subcategory Accuracy:** 56.79%  

This indicates:

- Strong alignment with human evaluation at the structural level  
- More difficulty in capturing nuanced subcategory distinctions  

## 🔎 Key Findings

From reasoning error distribution analysis:

- Most individual steps were **RR** (locally correct reasoning)  
- Frequent failures included:
  - **Misinterpretation of premises (~37.8%)**
  - **Error propagation (~28.9%)**

This reveals that LLMs often reason correctly at the micro-level, but errors compound across multi-step chains.

## 📄 Complete Project Documentation

- `LexiCoders_CSE576NLP_Final_Report.pdf`