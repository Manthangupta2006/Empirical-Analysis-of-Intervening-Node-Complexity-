# Intervening Node Complexity in Natural Language Dependencies

## Overview

This project investigates the structural complexity of words that occur between syntactic heads and their dependents in dependency trees. Using multilingual Universal Dependencies (UD) treebanks, the study examines whether intervening nodes tend to be structurally simpler than the average token in a sentence.

The analysis focuses on three key properties:

* Part-of-Speech (UPOS) distribution
* Node arity (number of syntactic children)
* Phrase length (subtree size)

The findings provide empirical evidence supporting **Dependency Distance Minimization (DDM)** and suggest that natural languages prefer structurally simple material between syntactically related words.

---

## Research Question

What types of nodes intervene between a head and its dependent in natural language dependency structures, and are these intervening nodes structurally simpler than typical sentence tokens?

---

## Dataset

The study uses multilingual Universal Dependencies treebanks, including:

* English (EWT)
* Hindi (HDTB)
* Spanish (AnCora)
* French (GSD)
* German (GSD)
* Italian (ISDT)
* Russian (SynTagRus)
* Chinese (GSDSimp)
* Turkish (BOUN)
* Japanese (GSD)

Total corpus size:

* 177,678+ sentences
* 3.4M+ tokens

---

## Methodology

### Intervening Node Extraction

For every dependency arc:

Head → Dependent

all tokens occurring between the head and dependent positions are identified as intervening nodes.

Punctuation tokens are excluded.

For each intervener, the following properties are computed:

### 1. UPOS Category

Universal Part-of-Speech tag:

* NOUN
* VERB
* ADV
* ADJ
* DET
* PRON
* etc.

### 2. Node Arity

Number of direct syntactic dependents:

Arity(node) = Number of Children

### 3. Phrase Length

Subtree size rooted at the node:

Phrase Length = Number of Tokens in Subtree

---

## Hypotheses

### H1: POS Hypothesis

Intervening nodes are dominated by structurally light categories such as:

* NOUN
* ADV
* DET

rather than structurally heavy categories such as:

* VERB
* SCONJ

### H2: Arity Hypothesis

Intervening nodes have fewer syntactic dependents than average sentence tokens.

### H3: Phrase-Length Hypothesis

Intervening nodes head smaller subtrees than average sentence tokens.

---

## Pipeline

```text
Dependency Treebank
        │
        ▼
Extract Dependency Arcs
        │
        ▼
Identify Interveners
        │
        ▼
Compute Features
 ├── UPOS
 ├── Arity
 └── Subtree Size
        │
        ▼
Statistical Analysis
        │
        ▼
Visualization & Results
```

---

## Statistical Analysis

### Enrichment Ratio

Measures whether a POS category is over- or under-represented among interveners:

ER(u) = P(u | Intervener) / P(u | All Tokens)

Interpretation:

* ER > 1 → Over-represented
* ER < 1 → Under-represented

### Hypothesis Testing

One-sided t-tests are performed to compare:

* Mean arity of interveners vs all tokens
* Mean subtree size of interveners vs all tokens

Effect size is measured using Cohen's d.

---

## Key Results

### POS Distribution

Over-represented among interveners:

* NOUN (ER ≈ 1.30)
* ADV (ER ≈ 1.65)
* DET (ER ≈ 1.08)

Under-represented:

* VERB (ER ≈ 0.54)
* PRON (ER ≈ 0.78)
* SCONJ/CCONJ (ER ≈ 0.83)

### Arity Analysis

* Mean Arity (Interveners): ≈ 0.84
* Mean Arity (All Tokens): ≈ 1.84
* p < 0.001

Interveners contain substantially fewer syntactic dependents.

### Phrase Length Analysis

* Mean Subtree Size (Interveners): ≈ 2.12
* Corpus Mean Subtree Size: ≈ 4.5
* p < 0.001

Over 83% of interveners have subtree sizes ≤ 3.

---

## Technologies Used

* Python
* Pandas
* NumPy
* SciPy
* Matplotlib
* Conllu

---

## Repository Structure

```text
.
├── treebanks/
├── notebooks/
├── figures/
├── results/
├── analysis.py
├── requirements.txt
└── README.md
```

---

## Running the Project

Install dependencies:

```bash
pip install conllu pandas scipy matplotlib seaborn
```

Run analysis:

```python
df = analyze_treebank("treebanks/en_ewt-ud-train.conllu")

test_hypothesis(df, "arity")
test_hypothesis(df, "size")

er = enrichment_ratio(df)

plot_enrichment(er)
```

---

## Key Contributions

* Developed a multilingual dependency analysis framework.
* Extracted and characterized intervening nodes across dependency arcs.
* Computed structural complexity metrics using arity and subtree size.
* Performed statistical validation of Dependency Distance Minimization predictions.
* Generated visualizations highlighting universal patterns across languages.

---

## Authors

**Manthan Gupta**
Indian Institute of Technology Kanpur

**Diya Gupta**
Indian Institute of Technology Kanpur

