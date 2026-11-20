## Pinto et al., ICLR 2026 Gen² Workshop

**Structured and interpretable patient embeddings from Single-Cell Foundation Models**

[Paper: OpenReview](https://openreview.net/pdf?id=R69blzZXnr)

### Research Question

- 能否利用Single-Cell Foundation Models（单细胞基础模型）学习患者级表征？
    
- 能否使Patient Embedding（患者表征）的不同维度对应可解释的生物学概念，而不只是抽象的数字？
    
- 这些表征能否用于肿瘤亚型、分级预测，并揭示肿瘤微环境差异？
    

### Methods

**1. SCOPE模型结构**

输入：患者的单细胞基因表达数据。

- **TranscriptFormer**：预训练单细胞基础模型，将每个细胞编码为Cell Embedding。
    
- **GM-VAE（高斯混合变分自编码器）**：学习细胞亚群的分布，通过软聚类权重整合细胞表征，获得患者级表征。
    
- **Concept Bottleneck（概念瓶颈）**：将患者表征映射到预定义的生物学概念空间，提高可解释性。
    

概念层包含：

- 132个Gene Signatures（基因特征集），得到Gene Scores。
    
- 进一步映射到43个肿瘤免疫微环境相关概念，得到Pathway Scores。
    

**2. 模型训练**

- **Continual Pre-training（持续预训练）**：使用约150万个来自癌症、健康及炎症相关数据的细胞，进一步训练TranscriptFormer，使其适应疾病研究。
    
- **GM-VAE**：通过重构损失、KL散度及正则化学习细胞表征的混合分布。
    
- **Supervised Contrastive Loss（监督对比损失）**：使相同疾病或亚型的患者表征更接近，不同疾病患者的表征更远。
    
- GM-VAE和Concept Projector从头训练；整体训练结合生成式目标与监督对比目标。
    

### Evidence Chain

|Figure / Table|核心发现|
|---|---|
|**Fig. 1**|提出SCOPE：TranscriptFormer → GM-VAE → Concept Bottleneck → 可解释的患者表征|
|**Fig. 2a–d**|比较不同方法的患者UMAP；SCOPE具有相对更好的批次混合表现|
|**Table 1**|Gene Scores预测乳腺癌亚型：Accuracy=0.68、F1=0.67；预测肿瘤分级：Accuracy=0.63、F1=0.62，优于所比较的基线|
|**Fig. 2e**|原发性与浸润性乳腺癌之间，CD4⁺ T cell、Mast cell（肥大细胞）、Endothelial cell（内皮细胞）及T cell相关概念的评分存在显著差异|

### Key Concepts & Questions

**1. GM-VAE与PaSCient的Aggregator有什么区别？**

- PaSCient：利用Attention直接加权聚合细胞向量。
    
- SCOPE：通过GM-VAE学习细胞所属亚群的概率，结合不同亚群的表征与相对丰度生成患者向量。
    
- SCOPE不仅考虑细胞表达状态，也显式建模细胞亚群组成。
    

**2. Concept Bottleneck为什么能提高可解释性？**

- 普通Embedding的各个维度通常没有明确生物学含义。
    
- Concept Bottleneck将表征映射为基因特征集及通路相关评分。
    
- 例如，T cell exhaustion（T细胞耗竭）或NK cell cytotoxicity（NK细胞毒性）等概念，可以用于解释患者之间的差异。
    
- 但概念评分是模型推断的特征活性，不等于直接测量了通路活性或证明了调控机制。
    

**3. SCOPE为什么不直接使用TranscriptFormer的Cell Embedding？**

- TranscriptFormer主要学习单个细胞的表达特征。
    
- 患者疾病状态还取决于不同细胞亚群的组成及状态。
    
- 因此需要GM-VAE完成细胞级到患者级的整合，再通过Concept Bottleneck提取可解释特征。
    

**4. Gene Scores和Pathway Scores有什么区别？**

- Gene Scores：132个较细粒度的基因特征集评分。
    
- Pathway Scores：43个较高层次的生物学概念评分。
    
- Gene Scores在本文的预测任务中表现更好；Pathway Scores更便于直接解释生物学意义。
    
- 说明预测性能与可解释性之间可能存在权衡。
    

### Limitations

- 主要在138名乳腺癌患者、274,555个免疫细胞的数据上验证，疾病及队列覆盖有限。
    
- 受计算资源限制，持续预训练仅进行了一个Epoch（训练轮次）。
    
- 模型可解释性依赖预先定义的Gene Signatures和生物学概念，可能遗漏未知的疾病相关程序。
    
- 生物学概念评分与已有研究一致，不等于已经完成因果机制验证。
    
- 对不同癌种、独立临床队列及治疗应答预测的泛化能力仍需进一步评估。
    

### Conclusion

SCOPE通过基础模型、GM-VAE和Concept Bottleneck，将单细胞表达信息转换成结构化、可解释的患者表征。

