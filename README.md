# 🧹 TextDetox @ PAN CLEF 2025: Multilingual Text Detoxification

<div align="center">

[![CLEF 2025](https://img.shields.io/badge/CLEF-2025-blue?style=for-the-badge)](https://clef2025.clef-initiative.eu/)
[![PAN 2025](https://img.shields.io/badge/PAN-2025-orange?style=for-the-badge)](https://pan.webis.de/clef25/pan25-web/text-detoxification.html)
[![HuggingFace](https://img.shields.io/badge/🤗_HuggingFace-textdetox-yellow?style=for-the-badge)](https://huggingface.co/textdetox)
[![CodaLab](https://img.shields.io/badge/CodaLab-Leaderboard-green?style=for-the-badge)](https://codalab.lisn.upsaclay.fr/competitions/22396)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey?style=for-the-badge)](https://creativecommons.org/licenses/by/4.0/)

**The second edition of the Multilingual Text Detoxification shared task at PAN @ CLEF 2025**  
*15 Languages · 26 Teams · Dual Evaluation (Automatic + LLM-as-a-Judge)*

[**📄 Overview Paper**](https://iris.unibocconi.it/bitstream/11565/4079002/1/paper_278.pdf) · [**🤗 Starter Kit**](https://huggingface.co/collections/textdetox/textdetox-2025-starter-kit) · [**🌐 Task Page**](https://pan.webis.de/clef25/pan25-web/text-detoxification.html) · [**💬 Google Group**](https://groups.google.com/g/textdetox-clef2025)

</div>

---

## 📌 Overview

**Text detoxification** is a *text style transfer* (TST) task: given a toxic sentence, rewrite it in a non-toxic way while preserving the original meaning as faithfully as possible. Unlike simple content moderation (blocking toxic text), detoxification enables a **proactive** response — offering the author a neutral reformulation of their message.

TextDetox 2025 is the second iteration of the PAN shared task, extending coverage from **9 to 15 languages** and introducing a **cross-lingual zero-shot challenge** for 6 new languages with no parallel training data.

```
Input  → "What a f**k is this about?"
Output → "What is this about?"

Input  → "Was für ein besch**senes Jahr"
Output → "Was für ein schlechtes Jahr."

Input  → "卧槽，抓到了！"
Output → "天啊，抓到了！"
```

> ⚠️ *This repository and paper contain rude texts used solely as illustrative examples.*

---

## 🌍 Languages

| Challenge | Languages | Parallel Training Data |
|---|---|---|
| **Multilingual (AvgP)** | English · Spanish · German · Chinese · Arabic · Hindi · Ukrainian · Russian · Amharic | ✅ 400 pairs/language |
| **Cross-lingual (AvgNP)** | Italian · French · Hebrew · Hinglish · Japanese · Tatar | ❌ Zero-shot transfer only |

The cross-lingual challenge specifically targets **low-resource and morphologically diverse languages**, including a code-switching variety (Hinglish) and a minority language (Tatar).

---

## 🗂️ Key Resources

### 🤗 HuggingFace Hub — [`textdetox`](https://huggingface.co/textdetox)

| Resource | Link | Description |
|---|---|---|
| **Starter Kit 2025** | [🤗 Collection](https://huggingface.co/collections/textdetox/textdetox-2025-starter-kit) | All models, datasets, and tools for the 2025 edition |
| **Parallel ParaDetox Dataset** | [🤗 Dataset](https://huggingface.co/datasets/textdetox/multilingual_paradetox) | 400 toxic–neutral pairs × 9 languages (training) |
| **Test Set** | [🤗 Dataset](https://huggingface.co/datasets/textdetox/multilingual_paradetox_test) | 600 toxic sentences × 15 languages |
| **Toxicity Classification Dataset** | [🤗 Dataset](https://huggingface.co/datasets/textdetox/multilingual_toxicity_dataset) | ~5,000 samples × 15 languages for classifier training |
| **Multilingual Toxic Lexicon** | [🤗 Dataset](https://huggingface.co/datasets/textdetox/multilingual_toxic_lexicon) | Toxic keyword lists for all 15 languages |
| **Toxic Spans** | [🤗 Dataset](https://huggingface.co/datasets/textdetox/multilingual_toxic_spans) | Span-level toxic annotations for 9 languages |
| **XLM-R Toxicity Classifier v2** | [🤗 Model](https://huggingface.co/textdetox/xlmr-large-toxicity-classifier-v2) | xlm-roberta-large fine-tuned for binary toxicity detection (15 langs) |
| **mBART Detox Baseline** | [🤗 Model](https://huggingface.co/textdetox/mbart-detox-baseline) | mBART seq2seq baseline fine-tuned on 9 languages |
| **mT0-XL Detox (Top 2024 System)** | [🤗 Model](https://huggingface.co/s-nlp/mt0-xl-detox-orpo) | Top-performing model from TextDetox 2024 (ORPO-aligned) |

### 💻 Code

| Repository | Description |
|---|---|
| [**pan-code / clef25**](https://github.com/pan-webis-de/pan-code/tree/master/clef25/text-detoxification) | Official baselines, evaluation pipeline, and submission code |
| [**textdetox_clef_2025**](https://github.com/textdetox/textdetox_clef_2025) | Annotation details, extended results, human evaluation data |
| [**Fine-tuning Colab Notebook**](https://colab.research.google.com/drive/1Wd_32qGpED5M3cfmDapKqOGplgLQ39xP?usp=sharing) | Google Colab: seq2seq fine-tuning walkthrough |

---

## 📊 New Datasets — Main Contributions

A major contribution of TextDetox 2025 is the creation of **six new parallel detoxification datasets** for previously uncovered languages, each built with rigorous manual annotation pipelines following the [ParaDetox](https://aclanthology.org/2022.acl-long.469.pdf) collection protocol.

### DetoxifyFR 🇫🇷 — French
- **600 pairs** sourced from [FrenchToxicityPrompts](https://aclanthology.org/2024.trac-1.12/) and Jigsaw Multilingual; fully manual annotation by a native French speaker (PhD in CL); LLM-based pre-filtering (Llama-3.1-70B) + Qwen2.5-72B validation.  
- Quality: **96%** of detoxified sentences rated non-offensive by LLM judge.

### DetoxifyIT 🇮🇹 — Italian
- **600 pairs** from Twitter (AMI/HODI EVALITA tasks) and Jigsaw Wikipedia; annotated by 3 native Italian NLP experts using a collaborative consensus review process; filtered via Perspective API.

### HeDetox 🇮🇱 — Hebrew
- **600 pairs** scraped from a popular Israeli news forum (rotter.net); LLM-based toxicity classification using SOL taxonomy; few-shot CoT prompting for detoxification followed by 2-phase manual correction; high inter-annotator agreement (mBERT cosine sim: **0.937**).

### Japanese 🇯🇵
- **600 pairs** from the [open2ch corpus](https://huggingface.co/datasets/p1atdev/open2ch); keyword-based filtering of 10,000 sentences; annotated by a native Japanese CS PhD student; ~60% of filtered candidates were explicitly toxic.

### Hinglish 🇮🇳 (Hindi–English code-switching)
- **600 pairs** from the aggression-annotated Hindi-English corpus (OAG/CAG categories, Facebook posts); preprocessing to remove mentions, links, and emojis; annotated by two native Hindi speakers with NLP expertise.

### TatDetox — Tatar
- **600 pairs** from VKontakte posts (Web Corpus of minority Russian languages); combined toxic-lexicon and sentiment-classifier filtering; annotated by two native Tatar speakers including an NLP expert; cross-validated for quality.

---

## ⚙️ Evaluation Metrics

The **Joint Score (J)** is the primary leaderboard metric, computed per sample as the product of three components, each in [0, 1]:

```
J = mean_i [ TOX(s_i, g_i, r_i) · SIM(s_i, g_i, r_i) · FL(s_i, g_i, r_i) ]
```

| Metric | Model | Description |
|---|---|---|
| **TOX** (Style Transfer Accuracy) | [`xlmr-large-toxicity-classifier-v2`](https://huggingface.co/textdetox/xlmr-large-toxicity-classifier-v2) | Non-toxicity probability, penalized if output is *more* toxic than source |
| **SIM** (Content Preservation) | [`LaBSE`](https://huggingface.co/sentence-transformers/LaBSE) | Weighted cosine similarity to both source input and human reference |
| **FL** (Fluency) | [`xCOMET-lite`](https://huggingface.co/myyycroft/XCOMET-lite) | MT-style quality metric over (source, output, reference) triplet |

> **2025 Update:** All three metrics were upgraded relative to TextDetox 2024 to incorporate human references (not just source-output similarity), greatly improving alignment with human judgments.

Additionally, a **LLM-as-a-Judge** leaderboard was provided using a fine-tuned [Llama-3.1-8B](https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct) (LoRA, trained on TextDetox 2024 + RUSSE 2022 human annotations) for content similarity and toxicity pairwise scoring.

---

## 🏆 Results

### Automatic Evaluation — Languages with Parallel Data (AvgP)

| Rank | Team | AvgP | EN | DE | RU | UK | AR | HI | ES | ZH | AM |
|:---:|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 🥇 | **ducanhhbtt** | **0.685** | 0.734 | 0.798 | 0.749 | 0.799 | 0.718 | 0.619 | 0.686 | 0.618 | 0.446 |
| 🥈 | **Team MetaDetox** | **0.685** | 0.742 | 0.766 | 0.753 | 0.798 | 0.732 | 0.629 | 0.719 | 0.611 | 0.415 |
| 🥉 | **sky.Duan** | **0.676** | 0.727 | 0.757 | 0.754 | 0.770 | 0.715 | 0.627 | 0.696 | 0.551 | 0.491 |
| 4 | Team Pratham | 0.676 | 0.729 | 0.750 | 0.755 | 0.776 | 0.724 | 0.631 | 0.696 | 0.533 | 0.486 |
| — | *baseline_mt0* | *0.675* | — | — | — | — | — | — | — | — | — |
| — | *Human References* | *0.854* | — | — | — | — | — | — | — | — | — |

### Automatic Evaluation — New Languages, Zero-Shot (AvgNP)

| Rank | Team | AvgNP | IT | JA | FR | HE | TT | HIN |
|:---:|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 🥇 | **ducanhhbtt** | **0.643** | 0.784 | 0.674 | 0.802 | 0.531 | 0.556 | 0.511 |
| 🥈 | **adugeen** | **0.623** | 0.761 | 0.640 | 0.785 | 0.479 | 0.582 | 0.491 |
| 🥉 | **Team MetaDetox** | **0.609** | 0.755 | 0.587 | 0.802 | 0.530 | 0.498 | 0.481 |
| 4 | Jiaozipi | 0.607 | 0.728 | 0.647 | 0.801 | 0.499 | 0.485 | 0.480 |
| — | *baseline_gpt4* | *0.579* | — | — | — | — | — | — |
| — | *baseline_mt0* | *0.572* | — | — | — | — | — | — |
| — | *Human References* | *0.847* | — | — | — | — | — | — |

### LLM-as-a-Judge — Languages with Parallel Data (AvgP)

| Rank | Team | AvgP | EN | DE | RU | UK | AR | HI | ES | ZH | AM |
|:---:|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 🥇 | **Team MetaDetox** | **0.812** | 0.893 | 0.919 | 0.829 | 0.791 | 0.826 | 0.785 | 0.823 | 0.813 | 0.626 |
| 🥈 | **ducanhhbtt** | **0.798** | 0.871 | 0.919 | 0.827 | 0.785 | 0.814 | 0.762 | 0.797 | 0.796 | 0.614 |
| 🥉 | **adugeen** | **0.775** | 0.794 | 0.888 | 0.792 | 0.791 | 0.790 | 0.773 | 0.765 | 0.783 | 0.597 |
| — | *Human References* | *0.822* | — | — | — | — | — | — | — | — | — |

### LLM-as-a-Judge — New Languages, Zero-Shot (AvgNP)

| Rank | Team | AvgNP | IT | JA | FR | HE | TT | HIN |
|:---:|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 🥇 | **adugeen** | **0.722** | 0.823 | 0.805 | 0.860 | 0.657 | 0.583 | 0.606 |
| 🥈 | **ducanhhbtt** | **0.720** | 0.842 | 0.820 | 0.889 | 0.681 | 0.495 | 0.592 |
| 🥉 | **humairafaridq** | **0.718** | 0.819 | 0.819 | 0.883 | 0.671 | 0.511 | 0.586 |
| — | *Human References* | *0.828* | — | — | — | — | — | — |

> **Key finding:** Several teams surpassed GPT-4 baselines and some even exceeded human reference quality in resource-rich languages (English, Spanish, Russian, Ukrainian, Hebrew), demonstrating the effectiveness of task-specific fine-tuning and advanced prompting over vanilla LLM prompting.

---

## 🔬 Participating Systems — Highlights

| Team | Approach |
|---|---|
| **ducanhhbtt** 🥇 | Gemma 3 12B + LoRA fine-tuning · few-shot retrieval · Chain-of-Thought · data augmentation |
| **Team MetaDetox** 🥇 (LLM-J) | DeepSeek CoT prompting · diverse rewrite generation · semantic + toxicity-based reranking |
| **adugeen** 🥇 (NP LLM-J) | Strong cross-lingual transfer, top performance on Ukrainian & zero-shot new languages |
| **sky.Duan** | Parallel architecture combining mT0-XL-detox-ORPO and Qwen3 |
| **Jiaozipi** | Ensemble of DeepSeek + Qwen + Kimi via RISE framework · few-shot hint engineering |
| **jellyproll** | mT0 baseline + targeted vocabulary substitution for Tatar & Japanese |
| **humairafaridq** | GPT-4o-mini + in-context learning only (3 lang-specific toxic→neutral examples per language) |
| **SVATS** | Comparison of Qwen2-7B vs Gemma-2 4B · full vs LoRA fine-tuning strategies |
| **Team Detox** | Rule-based toxic span masking + GPT-4o-mini few-shot prompting |
| **nikita.sushko** | SFT on MultiParaDetox + SynthDetoxM + custom synthetic data pipeline |
| **d1n910** | DeepSeek-R1 + Chain-of-Thought prompting |
| **Team Pratham** | MT0-XL + task-specific prompting + language-specific lexical filtering |

---

## 🧱 Baselines

All baseline code is available at [`pan-code/clef25`](https://github.com/pan-webis-de/pan-code/tree/master/clef25/text-detoxification):

| Baseline | Description | AvgP | AvgNP |
|---|---|:---:|:---:|
| **Duplicate** | Copy toxic input unchanged | 0.475 | 0.482 |
| **Delete** | Remove toxic keywords via [multilingual lexicon](https://huggingface.co/datasets/textdetox/multilingual_toxic_lexicon) | 0.536 | 0.510 |
| **Backtranslation** | NLLB-3.3B → en → `bart-base-detox` → NLLB back | 0.481 | 0.342 |
| **mT0-XL (fine-tuned)** | [`mt0-xl-detox-orpo`](https://huggingface.co/s-nlp/mt0-xl-detox-orpo) — top 2024 system | 0.675 | 0.572 |
| **GPT-4 (zero-shot)** | GPT-4-0613 prompted for detoxification | 0.637 | 0.579 |
| **GPT-4o (zero-shot)** | GPT-4o-2024-08-06 | — | — |
| **o3-mini (zero-shot)** | o3-mini-2025-01-31 | 0.562 | 0.484 |
| **LLaMA-70B (few-shot)** | Llama-3.1-70B-Instruct | — | — |

---

## 📐 Task Definition

TextDetox targets **explicit toxicity** only — sentences containing obscene or rude lexicon where meaningful neutral content is present and recoverable. Implicit toxicity (sarcasm, passive aggression, targeted hate without neutral content) is explicitly excluded.

**Evaluation is three-dimensional:**

```
Toxic sentence (s) → Detoxified output (g) ← Human reference (r)
        ↕ TOX              ↕ SIM                    ↕ FL
   Non-toxicity       Content fidelity           Fluency/naturalness
```

---

## 🗓️ Timeline

| Date | Event |
|---|---|
| April 25, 2025 | Registration closed |
| **May 8, 2025** | Test phase started (extended test data for new languages) |
| **May 23, 2025** | Final submissions deadline |
| May 30, 2025 | Participant paper submission |
| June 27, 2025 | Acceptance notification |
| July 7, 2025 | Camera-ready due |
| **Sept 9–12, 2025** | 🏛️ CLEF Conference, Madrid, Spain |

---

## 📜 Citation

If you use TextDetox 2025 data, models, or evaluation tools, please cite:

```bibtex
@inproceedings{dementieva2025textdetox,
  title     = {Overview of the Multilingual Text Detoxification Task at PAN 2025},
  author    = {Dementieva, Daryna and Protasov, Vitaly and Babakov, Nikolay and
               Rizwan, Naquee and Alimova, Ilseyar and Brun, Caroline and
               Konovalov, Vasily and Muti, Arianna and Liebeskind, Chaya and
               Litvak, Marina and Nozza, Debora and Shah Khan, Shehryaar and
               Takeshita, Sotaro and Vanetik, Natalia and Ayele, Abinew Ali and
               Schneider, Florian and Wang, Xintong and Yimam, Seid Muhie and
               Elnagar, Ashraf and Mukherjee, Animesh and Panchenko, Alexander},
  booktitle = {Working Notes of CLEF 2025 -- Conference and Labs of the Evaluation Forum},
  year      = {2025},
  url       = {https://iris.unibocconi.it/bitstream/11565/4079002/1/paper_278.pdf}
}
```

### Related Work

```bibtex
@inproceedings{logacheva-etal-2022-paradetox,
  title     = {{ParaDetox}: Detoxification with Parallel Data},
  author    = {Logacheva, Varvara and Dementieva, Daryna and others},
  booktitle = {Proceedings of ACL 2022},
  year      = {2022},
  url       = {https://aclanthology.org/2022.acl-long.469}
}

@inproceedings{dementieva-etal-2024-textdetox,
  title     = {Overview of the Multilingual Text Detoxification Task at {PAN} 2024},
  author    = {Dementieva, Daryna and others},
  booktitle = {Working Notes of CLEF 2024},
  year      = {2024},
  url       = {https://ceur-ws.org/Vol-3740/paper-223.pdf}
}

@inproceedings{dementieva-etal-2025-coling,
  title     = {Multilingual and Explainable Text Detoxification with Parallel Corpora},
  author    = {Dementieva, Daryna and others},
  booktitle = {Proceedings of COLING 2025},
  year      = {2025},
  url       = {https://aclanthology.org/2025.coling-main.535/}
}
```

---

## 👥 Task Committee

| Name | Affiliation |
|---|---|
| [Daryna Dementieva](https://dardem.github.io) *(Lead)* | Technical University of Munich |
| Nikolay Babakov | University of Santiago de Compostela |
| Naquee Rizwan | IIT Kharagpur |
| Caroline Brun | NAVER Labs Europe |
| Chaya Liebeskind | Jerusalem College of Technology |
| Arianna Muti | Bocconi University |
| Debora Nozza | Bocconi University |
| Sotaro Takeshita | University of Mannheim |
| Xintong Wang | University of Hamburg |
| Seid Muhie Yimam | University of Hamburg |
| Ashraf Elnagar | University of Sharjah |
| Ilseyar Alimova | Skoltech / AIRI |
| Alexander Panchenko | Skoltech |
| Vitaly Protasov *(Evaluation)* | AI Research Institute, Moscow |

---

## 🔗 All Links at a Glance

| | |
|---|---|
| 🌐 Task page | https://pan.webis.de/clef25/pan25-web/text-detoxification.html |
| 📄 Overview paper | https://iris.unibocconi.it/bitstream/11565/4079002/1/paper_278.pdf |
| 🤗 HuggingFace org | https://huggingface.co/textdetox |
| 🤗 2025 Starter Kit | https://huggingface.co/collections/textdetox/textdetox-2025-starter-kit |
| 💻 Baselines & eval code | https://github.com/pan-webis-de/pan-code/tree/master/clef25/text-detoxification |
| 📊 CodaLab competition | https://codalab.lisn.upsaclay.fr/competitions/22396 |
| 📓 Fine-tuning notebook | https://colab.research.google.com/drive/1Wd_32qGpED5M3cfmDapKqOGplgLQ39xP |
| 💬 Google Group | https://groups.google.com/g/textdetox-clef2025 |
| 🏛️ CLEF 2025 | https://clef2025.clef-initiative.eu/ |

---

<div align="center">

Sponsored by **[Toloka.ai](https://toloka.ai/)** · CLEF Conference · Madrid, September 2025

*Making the web a less toxic place, one language at a time.* 🌱

</div>
