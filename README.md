# Data-Centric Curriculum Training of a GPT Language Model for Coherent Text Generation

## Individual Contributions

| Team Member | Roll Number | Contribution |
|------------|-------------|--------------|
| **P. Sarat** | BT2024179 | Developed the complete **Wikitext-103 training pipeline**, including preprocessing, tokenization, baseline training, and model performance analysis. |
| **Parth Jade** | BT2024034 | Built the **Wikitext + BookCorpus combined training pipeline**, including dataset integration, binary token generation, and intermediate-stage training. |
| **Sri Charan** | BT2024143 | Developed the complete **BookCorpus v2 refinement pipeline**, including dataset extraction, filtering, streaming preparation, and final-stage model training. |

---

# Project Objective

This project investigates whether **data quality and curriculum ordering** can improve text generation quality in a GPT-style language model without changing model architecture.

Instead of scaling parameters, we improved training through:

- structured pretraining
- corpus expansion
- dataset refinement
- progressive checkpoint transfer

---

# Training Pipeline

## Phase 1: Wikitext-103 Training

### Dataset
:contentReference[oaicite:0]{index=0}

### Pipeline
- merged train/validation/test splits
- cleaned formatting artifacts
- added section boundary markers
- normalized whitespace
- tokenized using GPT-2 BPE tokenizer (50,257 vocab)
- performed 90/10 train-validation split
- trained for **25,000 iterations**

### Output
- `wikitext_checkpoints.pt`
- `wikitext_configs.json`

---

# Phase 2: Combined Corpus Training

### Datasets
- :contentReference[oaicite:1]{index=1}
- :contentReference[oaicite:2]{index=2} (`all_books_300M.txt`)

### Pipeline
- re-encoded Wikitext from raw source
- encoded BookCorpus text separately
- generated:
  - `wiki_tokens.bin`
  - `book_tokens.bin`
- merged both into:
  - `combined_tokens.bin`
- total corpus size: **356M tokens**
- trained from **random initialization**

### Output
- `best_model.pt`

---

# Phase 3: BookCorpus Refinement

### Dataset Source
:contentReference[oaicite:3]{index=3} streaming API

### Pipeline
- streamed BookCorpus samples
- applied:
  - hard filtering
  - soft filtering
  - noise filtering
  - length filtering
- targeted **300M tokens**
- encoded into binary format
- resumed training from Phase 2 checkpoint

### Output
- `final_checkpoint.pt`

---

# Training Flow

Phase 1 → standalone Wikitext model  

Phase 2 → new training run using Wikitext + BookCorpus  

Phase 3 → resumes from Phase 2 checkpoint for final refinement  

---

# Final Results

Observed improvements across training phases:

- better coherence
- stronger sentence completion
- improved topic consistency
- cleaner prompt generation

Best validation losses:

- Wikitext: **3.6083**
- BookCorpus v1: **3.3716**
- BookCorpus v2: **3.3607**

---

# Repository Structure

```bash
.
├── Wikitext-103.ipynb
├── GPT_Training_Fixed.ipynb
├── Resume_Training.ipynb
├── bookcorpus_extractionv2.ipynb
├── best_model.pt
├── final_checkpoint.pt
└── README.md
```

---

# Tech Stack

- Python
- PyTorch
- Hugging Face Datasets
- NumPy
- GPT-2 Tokenizer
- Jupyter Notebook

---

# Conclusion

This project demonstrates that **better data sequencing and cleaning can improve smaller language models without architectural scaling.**
