# T Cell Epigenetic Regulation ：生物学背景知识

## 1. Chromatin & Epigenetic Regulation（染色质与表观遗传调控）

### 1.1 Chromatin Structure（染色质结构）

DNA与组蛋白共同构成chromatin（染色质），其基本包装单位是nucleosome（核小体）。

染色质的组织状态影响DNA能否被转录因子及其他调控蛋白接近。

- **Chromatin accessibility（染色质可及性）**：DNA被调控蛋白接近的程度。
    
- **Chromatin remodeling（染色质重塑）**：核小体位置或染色质结构发生变化，影响DNA可及性。
    
- **Histone modifications（组蛋白修饰）**：通过组蛋白的化学修饰参与染色质及基因表达调控。
    
- **DNA methylation（DNA甲基化）**：参与基因表达调控及部分表观遗传状态的维持。
    

需要注意：

- 染色质开放不代表基因一定高表达，还取决于TF结合、辅因子及细胞信号等因素。
    
- ATAC-seq主要测量染色质可及性，不能直接测量RNA表达、组蛋白修饰或DNA甲基化。
    

### 1.2 Epigenetic Stability（表观遗传状态稳定性）

- 不同T-cell states不仅具有不同的转录程序，也可能形成相对稳定的染色质可及性模式。
    
- 染色质重塑可能影响细胞后续的刺激响应、分化潜能及状态可塑性。
    
- 部分耗竭相关表观遗传变化较为稳定，因此解除抑制性受体信号不一定能够完全恢复原有的功能与分化状态。
    

**核心理解：表观遗传调控不仅影响当前的基因表达，也可能限制或促进后续细胞状态的转换。**

---

## 2. Cis-regulatory Elements（顺式调控元件）

### 2.1 Promoter、Enhancer与ACR

|概念|含义|
|---|---|
|Promoter（启动子）|通常位于TSS附近，参与转录起始|
|Enhancer（增强子）|可提高目标基因的转录活性，能够远距离发挥作用|
|ACR（可及染色质区域）|染色质相对开放的基因组区域，不一定具有增强子功能|
|TF motif（转录因子结合基序）|TF可能识别的短DNA序列模式|

它们并不是同一层次的概念：

- Enhancer和promoter是具有特定调控功能的基因组区域。
    
- TF motif是DNA序列模式，一个调控区域可以包含多个motifs。
    
- ACR描述染色质可及性，不能仅凭开放状态确定调控功能。
    

### 2.2 Distal Regulatory Elements（远端调控元件）

- **Proximal ACRs（近端可及染色质区域）**：通常根据与TSS的距离定义，常包含启动子附近的区域。
    
- **Distal ACRs（远端可及染色质区域）**：距离TSS较远，可能包含状态特异性的增强子。
    
- 不同T-cell states可能共享部分开放启动子，却使用不同的远端调控元件。
    
- 因此，远端ACRs能够提供重要的细胞身份和分化状态信息。
    

Giles 2022发现，distal ACRs比proximal ACRs和RNA表达更能区分研究中定义的T细胞亚群。

这并不意味着所有远端区域都具有增强子功能，也不代表远端区域在所有研究中都比启动子更重要。

### 2.3 Enhancer–Promoter Communication（增强子与启动子相互作用）

- Enhancer不一定调控距离最近的基因。
    
- DNA在细胞核内具有三维折叠结构，远端增强子可能通过空间接近参与目标基因的转录调控。
    
- 一个enhancer可能调控多个genes，一个gene也可能受到多个enhancers共同调控。
    
- Physical chromatin contact（染色质物理接触）不等于功能性调控关系。
    

---

## 3. TF-mediated Gene Regulation（转录因子介导的基因调控）

### 3.1 TF、Motif与Regulatory Program

基本调控关系：

`Cellular signaling → TF activation → TF binding → Enhancer/Promoter regulation → Gene transcription`

- **TF binding（转录因子结合）**：TF识别并结合特定DNA序列，参与促进或抑制基因转录。
    
- **Motif（基序）**：TF可能识别的DNA序列模式，不代表TF一定实际结合。
    
- **TF regulatory program（转录因子调控程序）**：多个TF、顺式调控元件及靶基因共同形成的调控体系。
    

需要注意：

- 一个TF可以调控多个基因。
    
- 一个enhancer可以受到多个TF共同调控。
    
- 相同TF家族的不同成员可能识别相似motifs。
    
- TF表达量升高不一定代表其调控活性增强。
    

### 3.2 Motif Activity与TF Binding

|指标|生物学含义|解释边界|
|---|---|---|
|Motif enrichment（基序富集）|某类TF motif在目标区域中出现得更频繁|不代表TF实际结合|
|Motif deviation（基序偏离）|含特定motif的区域，其可及性相对于预期背景的偏离程度|不等于TF蛋白活性或结合量|
|TF footprint（转录因子足迹）|TF可能占据DNA，造成结合位置附近的ATAC插入信号降低|属于间接结合证据|

TF footprint的基本原理：

- Tn5转座酶能够插入可及染色质区域。
    
- 当TF结合DNA时，可能形成空间阻碍，使结合位置的Tn5插入频率降低。
    
- 这种局部信号下降可能形成footprint。
    
- 分析时需要校正Tn5 sequence bias（序列偏好），避免将技术性信号变化误判为TF结合。
    

---

## 4. State-specific Enhancer Regulation（细胞状态特异性增强子调控）

### 4.1 Enhancer Landscape与T-cell States

不同T-cell states可能具有不同的enhancer landscapes（增强子景观），从而参与建立和维持状态特异性的基因表达程序。

这些差异主要体现在：

- 不同调控区域的染色质可及性。
    
- 不同TF motifs的富集及相关活性。
    
- 不同enhancers与目标genes的关联。
    
- 不同状态下基因表达调控的强度和方式。
    

因此，即使不同T-cell states表达同一个基因，它们也可能依赖不同的调控元件。

### 4.2 Shared与Context-specific Regulatory Programs

同一种T-cell state在不同组织中，可以同时具有：

**Shared regulatory programs（共享调控程序）+ Context-specific regulatory programs（环境特异性调控程序）**

- 共享程序与细胞状态的核心分子特征有关。
    
- 环境特异性程序可能受到组织信号、代谢条件及持续刺激的影响。
    
- 因此，不同癌种中的Tex可以共享核心耗竭相关调控特征，同时具有不同的染色质景观。
    

### 4.3 Super-enhancer（超级增强子）

Super-enhancer通常指由多个相邻增强子组成、具有较强调控特征的区域集合，常与细胞身份及关键调控基因有关。

需要区分：

- 传统super-enhancer分析常基于H3K27ac等调控信号。
    
- Riegel 2023采用的是借鉴super-enhancer思路的排序方法，根据基因关联的状态特异性marker peaks数量进行评分。
    
- 高评分意味着更多候选调控区域与该基因关联，不直接代表更高的RNA表达或更强的因果调控作用。
    

---

## 5. Linking Chromatin Accessibility to Gene Expression

### 5.1 Gene Activity与Gene Expression

- **Gene activity score（基因活性评分）**：根据基因相关区域的ATAC信号推断染色质活性。
    
- **Gene expression（基因表达）**：通过RNA-seq等技术直接测量转录本丰度。
    

Gene activity score ≠ RNA expression。

前者反映染色质相关的推断活性，后者反映实际检测到的RNA水平。

### 5.2 Enhancer–Gene Association（增强子与基因关联）

由于ATAC-seq不能直接确定开放区域的目标基因，需要借助其他信息推断调控关系。

主要思路：

- 比较ACR accessibility与gene expression的变化。
    
- 寻找在不同细胞状态之间具有相关性的调控区域与基因。
    
- 结合基因组距离、染色质接触及功能实验进一步评估关联。
    

两篇文章采用了不同策略：

- **Giles 2022**：多元回归与lmg relative importance，评估不同ACRs对跨亚群基因表达差异的相对解释贡献。
    
- **Riegel 2023**：整合scATAC-seq和scRNA-seq，根据peak accessibility与RNA expression的相关性预测peak-to-gene links（PGLs）。
    

需要注意：Riegel使用的ATAC和RNA并非同一细胞的直接配对测量，而是通过计算方法进行整合。

---

## 6. Functional Regulation of Enhancers（增强子的功能性调控）

### 6.1 为什么调控Enhancer而不直接敲除Gene？

- 完全敲除某些关键基因可能同时破坏其有益与有害功能。
    
- 不同enhancers可能在不同细胞状态或环境中发挥作用。
    
- 通过靶向状态特异性enhancers，有可能实现更精细的基因表达调节。
    

例如，PD-1既参与限制过度T细胞活化，也可能在部分情况下参与维持T细胞稳态。因此，调节特定环境下的PDCD1表达可能比完全敲除基因更精细。

### 6.2 Enhancer Perturbation（增强子扰动）

- **CRISPRi（CRISPR干扰）**：抑制候选调控区域，检验目标基因表达是否降低。
    
- **CRISPRa（CRISPR激活）**：激活候选调控区域，检验目标基因表达是否升高。
    

功能验证需要区分两个层次：

1. **Gene regulation（基因调控）**：干预增强子是否改变目标基因表达？
    
2. **Cell-state regulation（细胞状态调控）**：基因表达变化是否进一步影响T细胞分化、功能或命运？
    

---

## 7. Three Levels of Epigenetic Research（表观遗传研究的三个层次）

|层次|核心问题|常见证据|
|---|---|---|
|**Descriptive（描述性）**|哪些染色质区域开放？不同状态具有哪些调控特征？|ATAC-seq、DAPs、Motif enrichment|
|**Associative / Predictive（关联与预测）**|哪些调控区域可能影响哪些基因？哪些TF可能参与调控？|ACR–gene association、PGLs、Motif deviation|
|**Functional / Causal（功能与因果验证）**|干预调控元件是否改变基因表达或细胞功能？|CRISPRi/a、基因表达检测、功能实验|

核心区别：

`观察染色质差异 ≠ 证明增强子—基因调控关系 ≠ 证明调控机制对细胞功能具有因果作用`


