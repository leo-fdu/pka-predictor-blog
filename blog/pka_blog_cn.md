# 🧪 小规模 pKa 预测实验记录（GNN vs Fingerprint vs FG Baseline）

### 📌 介绍

在这个项目中，我使用一个基于公开数据整理得到的 pKa 数据集（清洗后共 **3109 条有效数据**），对不同类型的模型进行了简单对比实验。

该数据来源于公开的 IUPAC Digitized pKa Dataset。经过筛选后，本文仅保留了 **共轭酸（AH 类型）** 的数据进行建模，因此任务本质上是：

> 预测碱的共轭酸酸性（pKaH）

---

### ⚙️ 模型设置

本实验对比了四种方法：

- **GNN（图神经网络）**
- **Morgan Fingerprint + MLP**
- **Morgan Fingerprint + Random Forest（RF）**
- **Functional Group Baseline（FG）**：仅根据碱性官能团类别预测平均 pKa

数据划分方式包括：

- **Random Split**（随机划分）
- **Scaffold Split**（基于 Bemis–Murcko scaffold）

---

### 📊 实验结果（Best MAE）

| Model        | Random | Scaffold |
| ------------ | ------ | -------- |
| GNN          | 0.51   | 1.10     |
| Morgan + MLP | 0.92   | 1.54     |
| Morgan + RF  | 0.83   | 1.25     |
| FG Baseline  | 1.89   | —        |

---

### 🔍 结果分析

#### 1️⃣ Scaffold split 明显更困难

所有模型在 scaffold split 下性能均显著下降，例如：

- GNN：0.51 → 1.10
- MLP：0.92 → 1.54
- RF：0.83 → 1.25

这表明：

> scaffold split 引入了明显的结构分布偏移（distribution shift）

---

#### 2️⃣ GNN 表现最好

GNN 在两种划分下均取得最优性能，但在 scaffold split 下优势缩小。

这说明：

> GNN 的表达能力远超基于 fingerprint 的模型

---

#### 3️⃣ RF 优于 MLP 且有更好的泛化性能（在 fingerprint setting 下）

在 Morgan fingerprint 表征下，RF 的表现优于 MLP。

这说明：

> 在中小规模数据集上，传统机器学习模型仍然是强有力的 baseline

---

#### 4️⃣ FG baseline 的意义

虽然 FG baseline 表现较差（MAE ≈ 1.89），但它提供了一个纯化学规则驱动的参考：

> 模型性能必须显著优于该 baseline 才具有实际意义
