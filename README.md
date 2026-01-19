# PPG Artifact Detection (Systematic Review + Benchmark)

Detecting motion artifacts in **photoplethysmography (PPG)** signals — with a **systematic review**, a **shared benchmark**, and a new method (**CorTe**).

---

## ✨ Highlights

- 🔎 Systematic review of **50** artifact-detection algorithms in PPG literature  
- 🧪 Benchmark of **5 open-source** methods + **CorTe** (new, lightweight method)  
- 🧍‍♂️ Subject-independent evaluation via **LOSO cross-validation**  
- 📦 Reproducible pipeline + standardized metrics for fair comparison  

---

## 🔍 What this repo is about

Wearable PPG is powerful — but **motion artifacts** can dominate the signal and break downstream metrics (HR, HRV, morphology).
This repository collects:

- a **map of the field** (what people do, what they report, what data they use), and  
- a **benchmark framework** that evaluates available open-source methods under the *same* conditions. :contentReference[oaicite:1]{index=1}

---

## 📚 Systematic review (quick snapshot)

From the reviewed literature (Dec 1999 → Nov 27, 2024):
- **58%** of studies use **proprietary datasets**
- **78%** use **PPG-only** input (no accelerometer)
- **72%** use **fixed-length windows**
- **86%** output **binary labels**
- only **16%** are **open-source** (eligible for benchmarking) :contentReference[oaicite:2]{index=2}

---

## 🧪 Benchmark at a glance

### Dataset
Benchmark dataset is derived from **PPG-DaLiA** (real-life activities, wrist PPG @ 64 Hz).  
Ground truth comes from **sample-level artifact annotations** released with SEGADE (matched via exact window alignment). :contentReference[oaicite:3]{index=3}

### Evaluation
- **LOSO-CV** (leave-one-subject-out)
- Train/val split inside each fold (subject-wise separation)
- Standard metrics: accuracy, sensitivity, specificity, precision, F1-score, Cohen’s κ :contentReference[oaicite:4]{index=4}

---

## 🧠 Algorithms included

Benchmarked methods (open-source / available models):
- **VitalSQI** (rule-based SQI approach)
- **SEGADE** (deep learning, sample-level segmentation)
- **Tiny-PPG** (lightweight deep learning, sample-level segmentation)
- **DeepBeat** (window-level quality prediction; evaluated with pretrained model)
- **Pulse-SVM** (beat-level quality classification; evaluated with pretrained model)
- **CorTe** *(this work)*: template-based pulse correlation + thresholding (fast & interpretable) :contentReference[oaicite:5]{index=5}

---

## 🧾 Key takeaways (no fluff)

- Learning-based methods generally perform best, but trade-offs differ:
  - **Tiny-PPG** shines on **specificity / precision**
  - **Pulse-SVM** leads on **sensitivity**
  - **SEGADE** is the most balanced (strong **F1** and **κ**) :contentReference[oaicite:6]{index=6}
- Window-level methods can be penalized when evaluated sample-wise (granularity mismatch).
- **CorTe** is a strong lightweight option when compute or interpretability matters. :contentReference[oaicite:7]{index=7}

---

## 📁 Repository structure


```text
.
├─ data/                      # dataset pointers/scripts (no raw data)
├─ src/
│  ├─ preprocessing/          # filtering, windowing, pulse extraction
│  ├─ ground_truth/           # alignment + label handling
│  ├─ models/                 # wrappers for each algorithm
│  ├─ evaluation/             # metrics + LOSO-CV
│  └─ utils/
├─ notebooks/                 # exploration + figures
├─ scripts/
│  ├─ build_benchmark_dataset.*
│  ├─ run_loso_benchmark.*
│  └─ make_figures.*
└─ results/                   # generated outputs (optional; usually gitignored)
