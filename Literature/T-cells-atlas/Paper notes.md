
# T Cell Atlas：阅读笔记

## 01. Zheng et al., Science 2021

**Pan-cancer single-cell landscape of tumor-infiltrating T cells**

[DOI: 10.1126/science.abe6474](https://doi.org/10.1126/science.abe6474)

### Research Question（研究问题）

- 不同癌种中，肿瘤浸润T细胞具有怎样的异质性？
    
- CD8⁺/CD4⁺ T细胞有哪些分化状态和潜在转换路径？
    
- T细胞组成是否与癌种特征及患者临床结局相关？
    

### Methods（研究方法）

- **数据**：21种癌症、316名供者的scRNA-seq数据。
    
- **细胞图谱**：聚类、marker genes注释、跨癌种比较。
    
- **状态转换**：Pseudotime（伪时间）、RNA velocity（RNA速度）、TCR克隆分析。
    
- **调控机制**：TF（转录因子）、Regulon（调控子网络）。
    
- **临床关联**：T细胞组成与患者特征、预后分析。
    

### Key Findings（核心发现）

1. **T细胞异质性**：不同癌种共享部分T细胞状态，但其组成存在癌种差异。
    
2. **CD8⁺ T细胞**：存在多条潜在耗竭分化路径，Trm相关状态可能参与向Tex的转变。
    
3. **CD4⁺ T细胞**：识别出不同辅助性和调节性状态，包括TNFRSF9⁺ Treg。
    
4. **肿瘤反应性**：pTRTs（潜在肿瘤反应性T细胞）与部分耗竭相关状态密切联系。
    
5. **临床意义**：T细胞状态及组成与肿瘤特征、患者预后相关。
    

### Evidence Chain（证据链）

`跨癌种单细胞图谱 → 识别T细胞亚群 → 推断分化轨迹与调控程序 → 比较癌种差异 → 关联临床特征`

---

## 02. Chu et al., Nature Medicine 2023

**Pan-cancer T cell atlas links a cellular stress response state to immunotherapy resistance**

[DOI: 10.1038/s41591-023-02371-y](https://doi.org/10.1038/s41591-023-02371-y)

### Research Question（研究问题）

- 肿瘤T细胞是否存在尚未充分认识的功能状态？
    
- T细胞应激反应是否与ICB（免疫检查点阻断）抵抗有关？
    

### Methods（研究方法）

- **数据**：16种癌症、308,048个T细胞转录组。
    
- **图谱构建**：整合scRNA-seq，细分CD4⁺/CD8⁺ T细胞状态。
    
- **特征分析**：差异表达、Gene signatures（基因特征集）。
    
- **空间验证**：空间分析定位T_STR细胞。
    
- **临床关联**：结合ICB治疗前后及应答信息。
    
- **工具**：建立T细胞参考图谱及TCellMap注释工具。
    

### Key Findings（核心发现）

1. **T细胞异质性**：进一步识别Tfh、Treg、增殖T细胞等群体的内部异质性。
    
2. **T_STR状态**：发现具有Heat shock response（热休克反应）特征的T细胞状态。
    
3. **空间分布**：T_STR常见于淋巴细胞聚集区域或潜在TLS（三级淋巴结构）附近。
    
4. **ICB抵抗**：治疗后肿瘤内T细胞的应激相关基因表达升高，在非应答肿瘤中尤为明显。
    
5. **资源价值**：提供可用于后续研究的T细胞参考图谱和注释工具。
    

### Evidence Chain（证据链）

`跨癌种T细胞图谱 → 发现T_STR → 应激基因特征分析 → 空间定位 → ICB治疗前后与R/NR比较 → 提出与治疗抵抗的联系`

---

## 03. Liu et al., Cell 2025

**A single-cell atlas reveals immune heterogeneity in anti-PD-1-treated non-small cell lung cancer**

[DOI: 10.1016/j.cell.2025.03.018](https://doi.org/10.1016/j.cell.2025.03.018)

### Research Question（研究问题）

- 为什么接受相似治疗的NSCLC（非小细胞肺癌）患者具有不同的病理应答？
    
- TIME（肿瘤免疫微环境）能否用于患者分型？
    
- T细胞状态能否进一步预测非MPR患者的复发风险？
    

### Methods（研究方法）

- **数据**：234名接受新辅助化疗联合免疫治疗的NSCLC患者，术后肿瘤样本。
    
- **测序**：scRNA-seq + scTCR-seq。
    
- **TIME分型**：根据免疫细胞组成识别患者亚型。
    
- **细胞分析**：比较NK、B细胞、Teff、Treg及Tex相关状态。
    
- **克隆分析**：TCR clonal expansion（克隆扩增）。
    
- **临床关联**：MPR（主要病理缓解）、RFS（无复发生存期）。
    

### Key Findings（核心发现）

1. **TIME异质性**：识别出5种TIME亚型，具有不同的MPR比例。
    
2. **治疗应答**：MPR患者中，FGFBP2⁺ NK/NK-like T、Memory B或Effector T等细胞相对富集。
    
3. **免疫抑制**：非MPR患者中CCR8⁺ Treg比例较高。
    
4. **T细胞克隆性**：非MPR患者内部存在不同的Tex相关细胞及Treg克隆扩增模式。
    
5. **复发风险**：Tex相关细胞中Texp（前体耗竭T细胞）的比例与RFS相关，可进一步识别部分复发风险较低的非MPR患者。
    

### Evidence Chain（证据链）

`治疗后TIME图谱 → 5种患者亚型 → MPR/非MPR细胞组成差异 → TCR克隆扩增分析 → Texp相关指标 → RFS分析`

---

## 三篇论文的联系

|论文|研究重点|主要贡献|
|---|---|---|
|Zheng 2021|T细胞异质性与分化|建立跨癌种T细胞状态图谱|
|Chu 2023|T细胞应激与ICB抵抗|识别T_STR及其临床关联|
|Liu 2025|TIME异质性与临床结局|TIME分型、T细胞克隆性与复发风险|

### 研究逻辑的递进

```
Zheng 2021
肿瘤T细胞有哪些状态？
         ↓
Chu 2023
新的应激状态是否与治疗抵抗相关？
         ↓
Liu 2025
免疫细胞状态与组成如何关联患者应答和预后？
```

### 最重要的三个认识

1. **细胞图谱不只是聚类**：更重要的是揭示状态异质性、分化关系和潜在调控机制。
    
2. **T细胞状态不等于功能结论**：Tex、T_STR、Treg具有不同的生物学含义，需要结合转录组、TCR及功能证据解释。
    
3. **细胞状态与临床结局的联系是研究重点**：从描述细胞异质性，逐渐走向解释免疫治疗抵抗、患者分型与预后。
    
