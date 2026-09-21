# ICB response scRNA-seq 数据收集

今天主要建立了 **ICB（Immune Checkpoint Blockade，免疫检查点阻断）+ scRNA-seq（单细胞 RNA 测序）+ clinical response（临床治疗反应）** 这一类研究的基础知识框架，并学习了如何从 review（综述）中系统寻找可用数据集。

## 1. ICB 是什么

**ICB = Immune Checkpoint Blockade（免疫检查点阻断）**。

它属于 **cancer immunotherapy（肿瘤免疫治疗）**。核心思想是阻断免疫系统中的抑制性 checkpoint pathway（免疫检查点通路），从而解除对 T cells（T 细胞）的抑制，增强抗肿瘤免疫反应。

常见 ICB 类型包括：

- **anti-PD-1（抗 PD-1）**
    
- **anti-PD-L1（抗 PD-L1）**
    
- **anti-CTLA-4（抗 CTLA-4）**
    

同一种治疗类型可以有多个具体药物。例如 anti-PD-1 是一种治疗策略，而 **nivolumab（纳武利尤单抗）**、**pembrolizumab（帕博利珠单抗）** 是具体药物。

所以层级是：

```text
Cancer immunotherapy（肿瘤免疫治疗）
        ↓
ICB（免疫检查点阻断）
        ↓
anti-PD-1 / anti-PD-L1 / anti-CTLA-4
        ↓
具体药物
```

## 2. Response 

常见分类：

```text
CR = Complete Response（完全缓解）
PR = Partial Response（部分缓解）
SD = Stable Disease（疾病稳定）
PD = Progressive Disease（疾病进展）
```

很多研究会进一步简化为：

```text
CR + PR
→ Responder（应答者）

SD + PD
→ Non-responder（无应答者）
```

但不同研究的定义可能不同，因此需要查看原文中的 response definition（疗效定义）。

## 3. Tumor Microenvironment, TME（肿瘤微环境）

TME 不是单纯指 tumor cells（肿瘤细胞），而是肿瘤周围和内部共同存在的整个“生态系统”，包括：

```text
Tumor cells（肿瘤细胞）
Immune cells（免疫细胞）
Fibroblasts（成纤维细胞）
Endothelial cells（内皮细胞）
Extracellular matrix（细胞外基质）
Blood vessels（血管）
Cytokines / chemokines（细胞因子 / 趋化因子）
```

ICB 与 TME 关系非常紧密，因为 ICB 主要不是直接杀死肿瘤，而是通过调节免疫反应发挥作用。

因此，不同患者的 TME 差异可能影响 ICB response（治疗应答）。

## 4. 为什么研究 Responder 和 Non-responder

核心问题不是单纯问：

> 这个药有没有效？

而是进一步问：

> 为什么有些患者有效，有些患者无效？

这类研究可以帮助理解：

- **response mechanism（应答机制）**
    
- **resistance mechanism（耐药机制）**
    
- **predictive biomarker（预测性生物标志物）**
    
- **patient stratification（患者分层）**
    
- **combination therapy（联合治疗）**
    

如果能找到治疗前就与 response 相关的细胞或分子特征，就可能帮助预测患者是否更可能从 ICB 获益。

## 5. scRNA-seq 为什么能研究 cell state（细胞状态）

scRNA-seq 可以获得每个细胞独立的 **gene expression profile（基因表达谱）**。

同一种 cell type（细胞类型）内部，也可能存在不同 cell states（细胞状态）。

例如两个都是 CD8+ T cells：

```text
Cell A
GZMB ↑
PRF1 ↑
NKG7 ↑
→ cytotoxic state（细胞毒状态）

Cell B
PDCD1 ↑
LAG3 ↑
HAVCR2 ↑
TOX ↑
→ exhausted-like state（耗竭样状态）
```

所以分析逻辑是：

```text
gene expression pattern（基因表达模式）
        ↓
marker genes / gene programs
        ↓
infer cell state（推断细胞状态）
```

scRNA-seq 不只是区分“是什么细胞”，还可以研究“这个细胞现在处于什么功能状态”。

## 6. ICB resistance（ICB 耐药）不只来自 TME

ICB resistance 可以来自两个层面：

```text
ICB resistance
├── tumor-intrinsic mechanisms（肿瘤内在机制）
│   └── cancer cell 本身的问题
│
└── tumor-extrinsic mechanisms（肿瘤外在机制）
    └── TME / immune microenvironment 的问题
```

例如：

- T-cell exhaustion（T 细胞耗竭）
    
- suppressive macrophages（抑制性巨噬细胞）
    
- 缺乏 T-cell infiltration（T 细胞浸润）
    
- antigen presentation defects（抗原呈递缺陷）
    

所以 scRNA-seq 的优势在于可以同时研究 tumor cells 和 surrounding immune/stromal cells（周围免疫/基质细胞）。

## 7. 当前数据收集任务的核心纳入标准

需要寻找：

> 接受 ICB（免疫检查点阻断）治疗的癌症患者，同时具有 scRNA-seq（单细胞 RNA 测序）数据和 clinical response information（临床治疗反应信息）。

可以概括为：

```text
Human cancer patients
+
ICB treatment
+
scRNA-seq
+
clinical response
```

最好还能知道：

- pre-treatment（治疗前）
    
- on-treatment（治疗中）
    
- post-treatment（治疗后）
    

因为不同时间点能回答不同问题。

## 8. Review（综述）怎么用

Review 更适合作为：

> **literature map（文献地图）**

而不是最终数据来源。

正确流程：

```text
Review
↓
Table / references
↓
Candidate original papers
↓
Original paper
↓
Supplementary materials
↓
GEO / SRA / EGA / other repository
↓
核实 dataset 信息
```

一个重要认识是：

> **Review 的 References 用来找论文，Original paper 的 Data availability 用来找数据。**

## 9. 搜 review 时，response 是重要关键词

只搜：

```text
ICB + scRNA-seq
```

范围会太宽，可能包含：

- mouse model（小鼠模型）
    
- checkpoint expression（免疫检查点表达）
    
- mechanism study（机制研究）
    
- 没有临床疗效信息的研究
    

因此更适合当前任务的搜索逻辑是：

```text
scRNA-seq
+
ICB
+
response / resistance
```

例如：

```text
"single-cell RNA sequencing" "immune checkpoint blockade" response review
```

## 10. 如何判断一篇 reference 是否值得纳入

不能只看标题。

需要逐步确认：

```text
Human patients（人类患者）？
        ↓
Received ICB（接受 ICB）？
        ↓
scRNA-seq？
        ↓
Clinical response available（有临床疗效信息）？
        ↓
Response 能否对应到 patient/sample？
```

全部满足，才真正接近老师需要的数据集。

## 11. 今天最重要的方法论收获

今天最大的认识是：

> 这项工作并不是简单地“搜数据集”，而是在建立  
> **biological context（生物学背景）— treatment（治疗）— single-cell data（单细胞数据）— clinical outcome（临床结局）**  
> 之间的对应关系。

同时也明确了两层工作应该分开：

```text
第一层：Candidate screening（候选文献筛选）
→ 快速判断值不值得继续查

第二层：Dataset verification（数据集核实）
→ 回到 original paper 和数据库
→ 核实 accession、response、pre/post、library、format 等信息
```

这样可以避免一开始就在不符合条件的论文上浪费大量时间。