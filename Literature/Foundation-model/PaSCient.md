## Liu et al., Cell Systems 2026

**Learning multi-cellular representations of single-cell transcriptomics data enables characterization of patient-level disease states**

[DOI: 10.1016/j.cels.2026.101570](https://doi.org/10.1016/j.cels.2026.101570)

### Research Question

- 能否将单细胞转录组信息整合为Patient Embedding（患者表征），用于研究患者级疾病状态？
    
- 能否识别对疾病预测具有重要贡献的细胞类型和基因？
    
- 学到的Patient Embedding能否迁移到疾病严重程度、治疗应答等新任务？
    

### Methods

**1. PaSCient模型结构**

输入：患者的单细胞基因表达矩阵。

- **Cell Embedder（细胞编码器）**：通过线性层，将每个细胞的基因表达转换为一个向量。
    
- **Cell Aggregator（细胞聚合器）**：通过Non-linear Attention（非线性注意力）加权整合多个细胞向量，生成Patient Embedding。
    
- **Classifier（分类器）**：根据Patient Embedding预测患者的疾病类别。
    

**2. 模型训练**

- 数据：约1,250万个细胞、2,790份患者样本。
    
- 监督标签：患者的疾病类别，而不是细胞类型。
    
- 训练过程：前向传播 → 疾病预测 → Cross-Entropy Loss（交叉熵损失）→ 反向传播。
    
- **End-to-end Training（端到端训练）**：Embedder、Aggregator和Classifier共同更新参数。
    
- 训练完成后，模型学会提取疾病相关的细胞特征，并将其整合成患者表征。
    

**3. 模型设计选择**

- Aggregator使用Attention，但不是Transformer；作者比较后发现Non-linear Attention性能更好。
    
- **Oversampling d+t**：同时针对Disease（疾病）和Tissue（组织）类别的不平衡进行过采样。
    
- 过采样增加少数类别被抽中的频率，不产生新的患者；下采样则会舍弃部分数据。
    
- Oversampling属于训练策略，不是神经网络结构本身。
    

**4. 可解释性**

使用Integrated Gradients（积分梯度，IG），计算每个细胞、每个基因对疾病预测的贡献，再聚合到细胞类型或基因层面。

### Evidence Chain

|Figure|结果与理解|
|---|---|
|**Fig. 1**|提出PaSCient，通过疾病分类任务学习患者级表征|
|**Fig. 2**|优于比较方法；非线性Attention与Oversampling d+t效果最佳|
|**Fig. 3**|Patient Embedding的UMAP同时呈现疾病与组织相关的分布差异|
|**Fig. 4A–B**|IG识别COVID-19相关的重要细胞（单核细胞）及基因（S100A8、S100A9、IFI27等）|
|**Fig. 4C–E**|检查归因分数与疾病相关细胞状态的联系，并比较健康与患病患者的归因差异|
|**Fig. 5**|未使用严重程度标签训练，但患者表征、疾病预测概率及细胞归因与轻重症相关|
|**Fig. S12**|迁移到黑色素瘤免疫治疗应答预测，Weighted F1=0.61|

### Key Concepts & Questions

**1. Patient Embedding是如何学出来的？**

- 不是预先存在的数据，也没有独立的真实Embedding标签。
    
- 模型通过疾病分类的监督任务，不断更新参数，学习如何提取、整合细胞特征。
    
- Patient Embedding是Aggregator输出、Classifier输入之前的中间表征。
    

**2. IG Attribution（归因）到底代表什么？**

- 正向归因：该特征提高模型对目标疾病的预测得分。
    
- 负向归因：该特征降低模型对目标疾病的预测得分，不等于统计学上的负相关。
    
- Figure 4A/B只保留正向归因；横轴的负值来自Log转换。
    
- **重要性高 ≠ 表达量高 ≠ 细胞数量多。**
    
- IG说明模型依赖哪些特征进行预测，不证明这些特征对疾病具有因果作用。
    

**3. Figure S12为什么需要重新训练Logistic Regression？**

因为PaSCient原来的Classifier只学习了疾病类别，并没有学习免疫治疗R/NR分类规则。

实际流程：

1. 用大量疾病数据预训练PaSCient。
    
2. 将新的黑色素瘤患者单细胞数据输入训练好的PaSCient，生成各自的Patient Embedding。
    
3. 固定PaSCient，使用新生成的Embedding及真实R/NR标签，训练Logistic Regression。
    
4. 在另一项独立研究的患者中测试应答预测效果。
    

**关键区别：复用的是预训练模型的参数，而不是直接复用原训练集中患者的Embedding。**

### Limitations

- 疾病与组织来源存在混杂，UMAP无法证明模型已将二者解耦。
    
- IG归因不代表基因差异表达、细胞丰度变化或因果调控。
    
- UMAP上的聚集和归因相关性，不能代替独立的生物学验证。
    
- 免疫治疗应答预测仅进行小规模跨队列验证（63名患者），预测性能有限。
    
- 模型依赖疾病标签进行监督训练；作者尚未实现自监督患者表征学习。
    

### Conclusion

PaSCient通过患者级疾病分类任务，学习将多个细胞的转录组信息整合为Patient Embedding，并利用IG解释疾病预测所依赖的细胞及基因特征。
