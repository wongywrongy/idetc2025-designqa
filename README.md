# idetc2025-designqa

## Problem Overview

This submission addresses Problem Statement 2: DesignQA Benchmark Challenge, hosted at the IDETC 2025 Hackathon.

Understanding technical design documents is a critical capability for engineering AI assistants, especially for compliance-driven domains like automotive or aerospace. However, Vision-Language Models (VLMs) currently struggle to accurately synthesize and apply complex rule-based knowledge from structured documents with embedded images and tables.

The **DesignQA** benchmark is designed to evaluate model performance on such tasks. It includes 1149 expert-crafted question-answer pairs grounded in the Formula SAE rulebook and MIT Motorsports engineering data.

Our goal is to build a system that can outperform existing models like GPT-4o and Gemini on the benchmark by:

* Improving information retrieval from the 140-page rulebook
* Enhancing comprehension of visual content (e.g., tables, diagrams)
* Reducing hallucination and improving answer consistency

## Approach Summary

We implement a fine-tuned Retrieval-Augmented Generation (RAG) pipeline supported by structured parsing and prompt engineering.

* Preprocessing:

  * Chunk the Formula SAE PDF rulebook by topic, section, and diagram context
  * Embed chunks using OpenAI or SentenceTransformers
* Retrieval:

  * Build a FAISS or Qdrant index
  * Use rerankers and filters to optimize relevance of returned passages
* Answering:

  * Use GPT-4o or Claude Opus for multi-step reasoning with rule context
  * Explore prompt tuning per benchmark segment (Extraction, Comprehension, Compliance)

## Architecture and Workflow

Pipeline:

1. PDF parsing and semantic chunking
2. Embedding generation and index building
3. Query-specific retrieval and context filtering
4. Prompt-driven QA generation and evaluation

Directory layout:

```
├── src/
│   ├── rag_pipeline.py         # Main RAG logic
│   ├── embed_rules.py          # Preprocessing and embedding
│   ├── answer_questions.py     # Final QA generation
├── data/
│   ├── rulebook_chunks.json    # Embedded chunks
│   └── questions.json          # Benchmark questions
├── evaluation/
│   ├── results_subset1.txt     # Per-subset scores
│   └── evaluate.py             # Scoring script
├── slides/                     # Presentation
└── README.md                   # This file
```

## Results

| Subset            | Accuracy (%) |
| ----------------- | ------------ |
| Retrieval         | XX.X         |
| Compilation       | XX.X         |
| Definition        | XX.X         |
| Presence          | XX.X         |
| Dimension         | XX.X         |
| Functional Perf.  | XX.X         |
| **Overall Score** | XX.X         |

* Accuracy computed using official DesignQA evaluation scripts
* Our method shows +X.X% improvement over GPT-4o on \[selected subset]

## Installation and Setup

```bash
git clone https://github.com/[your-org]/idetc2025-designqa.git
cd idetc2025-designqa
pip install -r requirements.txt
```

## How to Run

### Preprocess and Embed Rulebook

```bash
python src/embed_rules.py --input ./data/formula_sae.pdf
```

### Run QA Inference

```bash
python src/answer_questions.py --questions ./data/questions.json
```

### Evaluate Performance

```bash
python evaluation/evaluate.py --predictions ./results/answers.json
```

## Submission Contents

* `evaluation/results_subset*.txt`: Scores for each DesignQA subset
* `slides/final_presentation.pdf`: Slide deck overview
* `src/`: Pipeline and model interaction logic
* `notebooks/`: QA error analysis and sample prompts

## Limitations and Future Work

* Image understanding still relies on fallback OCR + captioning rather than full VLM reasoning
* Retrieval system could benefit from integrating document structure and visual layout as features
* Future work may include fine-tuning a VLM with synthetic DesignQA-style data under benchmark constraints

