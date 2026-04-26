# 🧪 Small-scale pKa Prediction Benchmark (GNN vs Fingerprint vs FG Baseline)

## 🇺🇸 English Version

### 📌 Introduction

In this project, I used a publicly available pKa dataset, which contained **3109 valid entries after cleaning**, to run a small benchmark across several model types.

The data comes from the public **IUPAC Digitized pKa Dataset**. After filtering, only **conjugate acid (AH-type)** entries were retained for modeling. Therefore, the task is essentially:

> Predicting the acidity of conjugate acids of bases (pKaH)

---

### ⚙️ Model Setup

Four approaches were compared in this experiment:

- **GNN (Graph Neural Network)**
- **Morgan Fingerprint + MLP**
- **Morgan Fingerprint + Random Forest (RF)**
- **Functional Group Baseline (FG)**: predicts the average pKa based only on basic functional group categories

Two data splitting strategies were used:

- **Random Split**
- **Scaffold Split** based on Bemis–Murcko scaffolds

---

### 📊 Results (Best MAE)

| Model        | Random | Scaffold |
| ------------ | ------ | -------- |
| GNN          | 0.51   | 1.10     |
| Morgan + MLP | 0.92   | 1.54     |
| Morgan + RF  | 0.83   | 1.25     |
| FG Baseline  | 1.89   | —        |

---

### 🔍 Result Analysis

#### 1️⃣ Scaffold split is clearly more difficult

All models show a clear performance drop under scaffold split:

- GNN: 0.51 → 1.10
- MLP: 0.92 → 1.54
- RF: 0.83 → 1.25

This indicates that:

> scaffold split introduces a clear structural distribution shift.

---

#### 2️⃣ GNN performs best

GNN achieves the best performance under both splitting strategies, although its advantage becomes smaller under scaffold split.

This suggests that:

> GNN has much stronger representational capacity than fingerprint-based models in this experiment.

---

#### 3️⃣ RF outperforms MLP and shows better generalization under the fingerprint setting

With Morgan fingerprint representation, RF consistently outperforms MLP.

This suggests that:

> Traditional machine learning models remain strong baselines on small- to medium-sized molecular datasets.

---

#### 4️⃣ Meaning of the FG baseline

Although the FG baseline performs poorly (MAE ≈ 1.89), it provides a purely chemistry-rule-based reference:

> A model needs to significantly outperform this baseline to be practically meaningful.
