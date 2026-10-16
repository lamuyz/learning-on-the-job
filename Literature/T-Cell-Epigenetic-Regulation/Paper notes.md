# T Cell Epigenetic Regulation：阅读笔记

## 01. Giles et al., Immunity 2022

**Human epigenetic and transcriptional T cell differentiation atlas for identifying functional T cell-specific enhancers**

[DOI: 10.1016/j.immuni.2022.02.004](https://doi.org/10.1016/j.immuni.2022.02.004)

### Research Question

- 人类不同T细胞分化状态具有怎样的转录与表观遗传特征？
    
- 健康供体建立的T细胞图谱能否用于解释疾病相关的T细胞状态？
    
- 哪些ACRs（可及染色质区域）参与调控T细胞状态特异性的基因表达？
    

### Methods

- **数据**：24名健康供体的14种T细胞亚群，Bulk ATAC-seq + RNA-seq。
    
- **表观遗传图谱**：ACR鉴定、聚类、差异可及性分析、TF motif分析。
    
- **分化与疾病关联**：转录与染色质调控模块分析；应用于Melanoma、BCC及自身免疫疾病相关数据。
    
- **调控关系预测**：ACR–gene association、多元回归、lmg relative importance（相对重要性）。
    
- **功能验证**：CRISPRi验证GZMB和CXCR3相关增强子的调控作用。
    

### Key Findings

1. **T细胞分化景观**：不同T细胞亚群具有特异性的转录与染色质可及性模式，distal ACRs（远端可及染色质区域）比proximal ACRs和RNA表达更能区分亚群。
    
2. **分化调控程序**：识别出与T细胞激活、记忆及效应分化相关的转录和表观遗传模块。
    
3. **耗竭相关状态**：健康供体外周血中的PD-1⁺CD39⁺ CD8⁺ T细胞具有与Tex相关的转录、染色质、蛋白及功能特征。
    
4. **疾病应用**：健康供体图谱能够帮助解释肿瘤浸润T细胞的状态及自身免疫疾病相关遗传变异。
    
5. **增强子调控**：ACR–gene模型能够预测基因表达变化；CRISPRi验证了部分GZMB和CXCR3增强子的功能。
    

### Evidence Chain

`健康供体T细胞分选 → 建立ATAC/RNA图谱 → 解析分化及调控程序 → 应用于疾病数据 → 预测ACR–gene关联 → CRISPRi功能验证`

---

## 02. Riegel et al., Molecular Cell 2023

**Integrated single-cell profiling dissects cell-state-specific enhancer landscapes of human tumor-infiltrating CD8+ T cells**

[DOI: 10.1016/j.molcel.2022.12.029](https://doi.org/10.1016/j.molcel.2022.12.029)

### Research Question

- 不同功能状态的肿瘤浸润CD8⁺ T细胞具有怎样的染色质及增强子景观？
    
- 不同癌种的Tex是否具有共同的耗竭调控程序及癌种特异性差异？
    
- 哪些enhancers和TFs可能参与调控不同T-cell states的基因表达？
    

### Methods

- **数据**：四种癌症及对照来源的scATAC-seq数据（26,479个CD8⁺ T cells）；整合公开scRNA-seq（38,356个细胞）。
    
- **染色质景观**：ArchR聚类、gene activity、差异开放区域分析。
    
- **调控机制**：TF motif deviation、TF footprinting、跨癌种比较。
    
- **耗竭轨迹**：Pseudotime分析染色质可及性、TF活性及gene activity的动态变化。
    
- **增强子关联**：scATAC/scRNA整合、peak-to-gene links（PGLs）、Hi-C数据比较、super-enhancer相关排序。
    
- **功能验证**：CRISPRa和CRISPRi验证PDCD1、TCF7相关增强子。
    

### Key Findings

1. **染色质异质性**：不同CD8⁺ T-cell states具有不同的染色质可及性及潜在TF调控程序。
    
2. **癌种差异**：不同癌种的Tex具有共同的耗竭特征，同时保留组织相关的染色质差异。
    
3. **共同耗竭轨迹**：推断出Tpex → Proliferating Tex → Terminal Tex的潜在状态变化路径，伴随染色质可及性、TF motif activity和gene activity的改变。
    
4. **增强子—基因关联**：通过scATAC/scRNA整合预测49,902条PGLs，并利用已知增强子及Hi-C数据提供外部支持。
    
5. **关键调控基因**：基于状态特异性关联增强子数量进行排序，识别TOX、TCF7、TBX21等重要候选基因。
    
6. **功能验证**：PDCD1增强子CRISPRa提高PD-1⁺细胞比例；TCF7增强子CRISPRi降低TCF1蛋白表达。
    

### Evidence Chain

`scATAC-seq染色质景观 → 识别T-cell states及TF调控特征 → 推断共同耗竭轨迹 → 整合scRNA-seq预测PGLs → 筛选关键调控区域 → CRISPRi/a功能验证`

---

## Key Concepts — Three Levels of Epigenetic Research

### 1. Descriptive（描述性研究）

**研究哪些表观遗传特征存在，以及不同细胞状态之间有何差异。**

- Chromatin accessibility：哪些染色质区域开放？
    
- Differential accessibility：哪些ACRs在不同T-cell states中存在差异？
    
- TF motif enrichment：哪些潜在TF结合基序富集？
    

### 2. Associative / Predictive（关联与预测）

**研究表观遗传特征与基因表达、细胞状态之间的潜在调控关系。**

- ACR–gene association：开放区域与哪些基因表达相关？
    
- TF motif activity：哪些潜在TF调控程序与细胞状态相关？
    
- Peak-to-gene links：哪些候选增强子可能调控目标基因？
    

### 3. Functional / Causal（功能与因果验证）

**通过实验干预，检验候选调控元件是否真正影响基因表达或细胞功能。**

- CRISPRi：抑制候选调控元件，观察目标基因表达是否下降。
    
- CRISPRa：激活候选调控元件，观察目标基因表达是否上升。
    
- Functional assays：进一步检验调控变化是否影响T细胞功能。
    

**核心区别：**

`观察染色质差异 ≠ 证明调控关系 ≠ 证明调控机制对细胞功能具有因果作用`