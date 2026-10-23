# eRNA & Enhancer Mechanisms: Literature Notes

## 01. Oguchi et al., Science 2024

**An atlas of transcribed enhancers across helper T cell diversity for decoding human diseases**

[DOI: 10.1126/science.add8394](https://doi.org/10.1126/science.add8394)

### Research Question

- 如何在单细胞水平识别eRNA transcription（增强子RNA转录），构建不同helper T-cell states（辅助性T细胞状态）的活性增强子图谱？
    
- 不同T细胞状态的enhancer transcription具有怎样的特异性？
    
- 能否利用转录增强子图谱定位免疫疾病相关遗传变异，并预测其靶基因？
    

### Methods

- **数据**：约100万个human CD4⁺ T cells；整合5′ scRNA-seq、单细胞染色质可及性数据及其他表观遗传数据。
    
- **增强子识别**：开发ReapTEC，利用5′ scRNA-seq中的RNA 5′端cap signature定位TSS，识别bidirectional eRNA transcription。
    
- **细胞状态分析**：单细胞聚类、分化轨迹分析、细胞状态特异性增强子转录分析。
    
- **多组学整合**：比较转录增强子与chromatin accessibility、组蛋白修饰及TF调控特征。
    
- **疾病关联**：GWAS、遗传力富集分析、LD分析，识别免疫疾病相关增强子。
    
- **调控关系预测**：Micro-C / RCMC分析染色质互作，结合ABC模型及表达关联预测enhancer–target gene links。
    
- **功能验证**：CRISPRa验证部分候选增强子的靶基因调控作用。
    

### Key Findings

1. **转录增强子图谱**：通过ReapTEC识别约6万个活性转录增强子，建立不同CD4⁺ T-cell states的增强子转录图谱。
    
2. **细胞状态特异性**：Bidirectionally transcribed enhancers具有明显的细胞类型及状态特异性，可辅助解析T细胞异质性与分化。
    
3. **表观遗传特征**：增强子转录与染色质可及性、活性组蛋白修饰存在联系，但反映的是不同层面的调控活动。
    
4. **疾病遗传学关联**：多种免疫疾病的遗传力及GWAS相关变异在特定T细胞状态的转录增强子中富集。
    
5. **增强子—靶基因联系**：结合高分辨率染色质互作数据，预测疾病相关增强子的候选靶基因；CRISPRa为部分调控关系提供功能证据。
    
6. **重复序列贡献**：部分增强子与TEs（转座元件）重叠，涉及LTR、SINE、LINE及DNA transposons，提示重复序列可能参与细胞状态特异性的调控景观。
    

### Evidence Chain

`5′ scRNA-seq → ReapTEC识别双向转录增强子 → 构建T细胞状态特异性图谱 → 整合表观遗传及GWAS数据 → 预测enhancer–gene links → CRISPRa功能验证`

---

## 02. Sasse et al., Nature Communications 2025

**Enhancer RNA transcription pinpoints functional genetic variants linked to asthma**

[DOI: 10.1038/s41467-025-57693-x](https://doi.org/10.1038/s41467-025-57693-x)

### Research Question

- 能否利用动态eRNA transcription定位与asthma（哮喘）相关的functional SNPs（功能性遗传变异）？
    
- SNP是否通过改变TF binding motifs及enhancer activity影响靶基因表达？
    
- 环境刺激、增强子调控与疾病遗传风险之间存在怎样的联系？
    

### Methods

- **数据**：BEAS-2B人支气管上皮细胞；GERA队列（16,274名哮喘患者、38,269名对照）。
    
- **SNP筛选**：GRO-seq检测动态eRNA transcription；Tfit定位双向转录中心μ；筛选μ附近的SNP。
    
- **遗传关联**：多变量Logistic regression、permutation testing、fine mapping及UK Biobank重复验证。
    
- **调控机制**：TF motif analysis、ATAC-seq、GR ChIP-seq及已有AHR占据数据。
    
- **增强子—靶基因联系**：GRO-seq / PRO-seq分析转录共变，Micro-C分析染色质空间接触。
    
- **功能验证**：Luciferase reporter assay、site-directed mutagenesis、CRISPR deletion及qRT-PCR。
    
- **刺激处理**：Dex、TNF、TCDD及WSP，研究糖皮质激素、炎症和环境污染物相关响应。
    

### Key Findings

1. **功能性SNP筛选**：利用动态eRNA transcription及μ定位，识别35个独立的哮喘关联候选SNP，其中24个属于high-confidence μ-SNPs。
    
2. **增强子活性验证**：9个高置信度候选增强子中，7个在reporter assay中重现了内源性eRNA的动态调控特征。
    
3. **GR–GCNT1机制**：rs149411423（C→T）破坏预测的GR binding motif，显著削弱Dex诱导的报告活性；CRISPR删除增强子进一步支持其调控内源性GCNT1。
    
4. **AHR–NR3C1机制**：rs258760（C→T）破坏预测的AHR binding motif，显著削弱TCDD及WSP诱导的报告活性。
    
5. **环境暴露与信号调控**：AHR配体预处理改变细胞后续的Dex相关转录响应，提示AHR与GR signaling之间存在功能联系。
    
6. **遗传关联与功能的区别**：GWAS关联显著性不等于直接调控功能；eRNA transcription可辅助优先筛选候选功能性变异。
    

### Evidence Chain

`GRO-seq识别动态增强子 → Tfit定位μ-SNP → GERA哮喘关联分析 → Reporter验证增强子活性 → TF motif及染色质互作分析 → SNP定点突变 → 功能机制验证`

**关键机制：**

- `rs149411423 C→T → GR motif受影响 → Dex-induced enhancer activity下降 → GCNT1调控`
    
- `rs258760 C→T → AHR motif受影响 → TCDD/WSP-induced enhancer activity下降 → NR3C1候选调控`
    

**证据限制：** 单碱基功能效应主要在reporter系统中得到验证；尚未通过内源性单碱基编辑完整证明SNP–TF–target gene–asthma的全部因果链。

---

## 03. Betti et al., Nature Communications 2025

_待读：以下为基于论文原文的预习概览，正式精读后完善。_

**Genetically regulated eRNA expression predicts chromatin contact frequency and reveals genetic mechanisms at GWAS loci**

[DOI: 10.1038/s41467-025-58023-x](https://doi.org/10.1038/s41467-025-58023-x)

### Research Question

- eRNA expression在多大程度上受到遗传变异调控？
    
- 能否利用genetically regulated eRNA expression预测chromatin contact frequency（染色质接触频率）？
    
- eRNA能否提供独立于常规基因表达的疾病遗传学信息，帮助解释GWAS loci？
    

### Methods

- **数据**：GTEx的49种细胞及组织类型，涉及14,471个转录增强子；整合BioVU、Hi-C、GWAS及UK Biobank数据。
    
- **遗传表达预测**：基于genotype建立eRNA和canonical gene的GReX（遗传调控表达量）预测模型。
    
- **染色质互作预测**：将GReX与Hi-C数据结合，利用deep learning预测enhancer–gene及enhancer–enhancer contact frequency。
    
- **疾病关联**：eRNA-based TWAS、eQTL分析及GWAS colocalization。
    
- **因果推断**：Mendelian randomization（孟德尔随机化），评估eRNA表达与疾病风险的潜在因果关系。
    
- **功能研究**：整合染色质调控标记及CRISPR perturbation，研究候选增强子与基因表达的关系。
    

### Key Findings

1. **eRNA遗传调控**：eRNA expression具有可预测的遗传成分，不同组织之间的预测性能存在差异。
    
2. **染色质互作预测**：eRNA与基因的GReX具有预测三维染色质接触频率的信息；模型在小脑数据中的测试集R²约为0.38。
    
3. **疾病相关eRNA**：eRNA-based TWAS识别出与schizophrenia（精神分裂症）等复杂性状相关的增强子转录信号，部分得到MR分析支持。
    
4. **增强子功能研究**：CRISPR扰动为部分疾病相关增强子与靶基因表达之间的调控关系提供实验支持。
    
5. **GWAS解释能力**：加入eRNA eQTL后，与调控变异共定位的GWAS信号数量，相比仅使用canonical gene eQTL增加约63%。
    

### Evidence Chain

`GTEx genotype + eRNA expression → 建立GReX预测模型 → 整合Hi-C预测chromatin contacts → eRNA-based TWAS → MR及colocalization → CRISPR功能支持`

**证据限制：** 统计因果推断和增强子区域扰动不等于直接证明eRNA分子本身具有因果调控功能。

