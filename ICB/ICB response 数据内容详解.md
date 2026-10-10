# ICB response 数据中的 patient、sample、timepoint 与 response

## 1. Patient 和 sample 不是一回事

**Patient（患者）** 是人。

**Sample（样本）** 是从患者身上在某个时间点取得、用于实验分析的材料，例如 tumor biopsy（肿瘤活检）或 blood sample（血液样本）。

因此：

```text
1 patient
↓
可以对应多个 samples
```

例如：

```text
Patient 01
├── baseline tumor biopsy（治疗前肿瘤活检）
├── on-treatment tumor biopsy（治疗中肿瘤活检）
└── post-treatment sample（治疗后样本）
```

所以：

```text
patient count ≠ sample count
```

这也是为什么一篇论文可能只有 32 位 patients（患者），但有 48 个 tumor biopsies（肿瘤活检样本）。

---

## 2. Baseline、on-treatment 和 post-treatment 分别是什么

### Baseline / pre-treatment（基线 / 治疗前）

指 ICB treatment（免疫检查点阻断治疗）开始之前。

可能同时存在两类 baseline 信息：

```text
baseline imaging（基线影像）
+
baseline sample（基线生物样本）
```

两者作用不同。

**Baseline imaging（基线影像）**：

> 记录治疗前肿瘤的初始状态，例如肿瘤大小、病灶数量等。

**Baseline sample（治疗前样本）**：

> 用于分析治疗开始前的 tumor microenvironment, TME（肿瘤微环境）、cell states（细胞状态）和 gene expression（基因表达）。

因此 baseline sample 特别适合研究：

**predictive biomarkers（预测性生物标志物）**

也就是：

> 在患者开始治疗之前，是否已经存在能够预测未来 response（治疗反应）的生物学特征。

---

## 3. On-treatment（治疗中）是什么意思

On-treatment 指：

> 患者已经开始接受治疗，但整个 treatment course（治疗过程）仍然在进行。

例如：

```text
9.10 开始治疗
↓
9.20 取样
↓
9.30 仍继续治疗
```

那么 9.20 取得的样本就是：

**on-treatment sample（治疗中样本）**

研究中通常更关注相对于治疗起点的时间，而不是具体日历日期。

例如：

```text
Day 0
Week 2
Week 4
Cycle 2 Day 1
```

即使不同患者在不同日期开始治疗，只要都在“治疗开始后第 10 天”取样，也可以统一归为某个 on-treatment timepoint（治疗中时间点）。

---

## 4. Post-treatment（治疗后）是什么

Post-treatment 更严格地说，是：

> 治疗已经结束、停止，或者完成某个既定治疗过程之后取得的样本。

因此时间轴可以理解为：

```text
Pre-treatment / Baseline
        ↓
Start treatment
        ↓
On-treatment
        ↓
End treatment
        ↓
Post-treatment
```

要注意，真实 ICB 治疗经常是多个 treatment cycles（治疗周期），所以“已经用过一次药”并不意味着就是 post-treatment。

---

## 5. Response 不是通过 scRNA-seq 判断出来的

**Response（治疗反应 / 疗效）** 通常是通过 clinical assessment（临床评估）得到的，而不是通过单细胞样本直接判断。

常见做法是：

```text
Baseline imaging（治疗前影像）
        ↓
开始治疗
        ↓
Follow-up imaging（随访影像）
        ↓
比较肿瘤变化
        ↓
RECIST 等疗效评价
        ↓
CR / PR / SD / PD
```

常见 response categories（疗效分类）：

```text
CR = Complete Response（完全缓解）
PR = Partial Response（部分缓解）
SD = Stable Disease（疾病稳定）
PD = Progressive Disease（疾病进展）
```

很多研究进一步分成：

```text
CR + PR
→ Responder（应答者）

SD + PD
→ Non-responder（无应答者）
```

---

## 6. Baseline image 和 baseline sample 是两条不同的数据线

可以把它们区分成：

```text
Clinical line（临床线）
Baseline imaging
↓
Follow-up imaging
↓
Response

Biological line（生物学线）
Baseline / on-treatment / post-treatment sample
↓
scRNA-seq
↓
TME / cell state / gene expression
```

两条线最后通过同一个 patient（患者）连接起来。

因此：

> **影像主要帮助判断 clinical response（临床疗效），而 scRNA-seq 主要帮助理解背后的 biological state（生物学状态）。**

---

## 7. 为什么 baseline sample 可以拥有 response label

虽然 baseline sample 是治疗前取得的，但患者未来的疗效是可以在之后知道的。

例如：

```text
Day 0
取 baseline sample
↓
开始 ICB
↓
几个月后影像显示 PR
```

那么这个治疗前样本就可以标记为：

> **sample from a future responder（来自未来应答患者的治疗前样本）**

它并不是说这个样本在取样时已经产生了 response，而是：

> 这个样本来自后来被证明会 response 的患者。

因此可以比较：

```text
baseline samples from responders
vs
baseline samples from non-responders
```

从而寻找 treatment前就存在的差异。

---

## 8. 为什么 on-treatment sample 有意义

On-treatment sample 的价值不在于直接判断 response，而在于研究：

> **治疗开始以后，肿瘤微环境和免疫细胞正在发生什么变化。**

例如：

```text
Week 2 on-treatment sample
↓
scRNA-seq
↓
发现某类 activated CD8+ T cells（活化 CD8+ T 细胞）增加
```

之后患者在 Week 8 影像上出现 PR。

于是研究者可以问：

> 治疗早期出现的某种 cell state（细胞状态）是否与未来 response 有关？

这类特征可能成为：

**early response biomarker（早期疗效生物标志物）**

所以 on-treatment 数据主要适合研究：

- early treatment response（早期治疗反应）
    
- treatment-induced changes（治疗诱导变化）
    
- response mechanism（应答机制）
    
- resistance mechanism（耐药机制）

---

## 9. Post-treatment sample 的作用

Post-treatment sample 主要用于观察：

> 治疗结束后，肿瘤和 TME（肿瘤微环境）最终变成什么状态。

例如可以研究：

- residual tumor biology（残留肿瘤生物学）
    
- persistent immune states（持续存在的免疫状态）
    
- treatment-resistant cell populations（治疗耐受细胞群）
    

因此三个时间点大致对应：

```text
Baseline
→ 治疗前是什么样？
→ prediction（预测）

On-treatment
→ 治疗正在作用时发生什么？
→ early response / mechanism（早期应答 / 机制）

Post-treatment
→ 治疗之后剩下什么？
→ outcome / residual biology（结果 / 残留生物学）
```

---

## 10. scRNA-seq 主要是在看什么

Baseline、on-treatment、post-treatment 的 samples，本质上都可以用来研究：

**Tumor Microenvironment, TME（肿瘤微环境）**

以及其中不同：

- cell types（细胞类型）
    
- cell states（细胞状态）
    
- gene expression programs（基因表达程序）
    
- immune composition（免疫细胞组成）
    

所以 scRNA-seq 主要不是在“诊断这个患者有没有 response”，而是在解释：

> **为什么患者会 response，为什么会 resistance，以及治疗过程中发生了什么。**

---

## 11. 完整逻辑


```text
Patient（患者）
│
├── Clinical assessment（临床评估）
│      ├── baseline imaging
│      └── follow-up imaging
│              ↓
│           response
│
└── Biological sampling（生物学取样）
       ├── baseline sample
       ├── on-treatment sample
       └── post-treatment sample
                ↓
             scRNA-seq
                ↓
      TME / cell states / pathways
```

关联两部分：

```text
Clinical outcome（临床结局）
+
Single-cell biology（单细胞生物学）
↓
理解 response / resistance
```
