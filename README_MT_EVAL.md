
English–Sepedi Machine Translation Evaluation

Project Title
Evaluation of NLLB and M2M100 Models on English–Sepedi Machine Translation using Corrected FLORES Dataset


Overview

This project evaluates the translation performance of two state-of-the-art multilingual machine translation models:

- `facebook/nllb-200-distilled-600M`
- `facebook/m2m100_418M`

The target language is Sepedi (Northern Sotho). We used the Corrected FLORES dev set to benchmark translation quality. The evaluation includes both quantitative metrics and qualitative error analysis.


Objectives

- Load a high-quality English–Sepedi evaluation dataset.  
- Generate translations using NLLB and fine-tuned M2M100 models.  
- Evaluate outputs using BLEU, chrF, and similarity scoring.  
- Identify translation challenges specific to Sepedi using manual error analysis.  



Dataset used in the project

- Source: Corrected FLORES  
- Columns:  
  - English: Source sentences  
  - Sepedi: Reference (ground truth) translations  
- Sample Size: 5 English–Sepedi sentence pairs used for evaluation  



facebook/nllb-200-distilled-600M - A distilled version of Meta’s No Language Left Behind model, supporting 200 languages
facebook/m2m100_418M - A 418M parameter multilingual model enabling direct many-to-many translation across 100 languages

Setup and Installation

Make sure the following packages are installed:

```bash
pip install transformers torch
pip install -U datasets huggingface_hub fsspec
pip install evaluate sacrebleu
```
from transformers import AutoTokenizer, AutoModelForSeq2SeqLM
import evaluate
from sacrebleu import corpus_bleu, corpus_chrf


How to Run

1. Launch the notebook  
2. Run all cells in sequence to generate `.txt` output files

Steps:
- Load the Corrected FLORES dataset
- Select and tokenize source texts
- Translate using each model:
  - Source lang: `"en"` (M2M100) or `"eng_Latn"` (NLLB)  
  - Target lang: `"nso"` (M2M100) or `"nso_Latn"` (NLLB)
- Generate and decode translations
- Evaluate using BLEU and chrF
- Use `difflib.SequenceMatcher` for similarity scoring
- Save all results to a `.txt` file


Evaluation Metrics

- BLEU: N-gram overlap between prediction and reference  
- chrF: Character-level precision and recall  
- Similarity Score: Uses `difflib` ratio (0.0 to 1.0)  
- Error Analysis: Logs worst-performing translations for manual inspection  



Output

- Detailed `.txt` report containing:  
  - Source, reference, and predicted translations  
  - Similarity scores  
  - BLEU and chrF scores  
  - 5 lowest-scoring translation examples  

---

Challenges Faced

- Language token mismatches (`nso` vs `nso_Latn`)  
- Copying behavior (predicted == source)  
- Limitations of BLEU and chrF in capturing Sepedi fluency  
- Limited parallel training data for Sepedi  


References

- Hugging Face Transformers
- Meta NLLB Project 
