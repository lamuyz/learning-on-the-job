# eRNA & Enhancer Mechanisms：生物学背景知识

## 1. Enhancer RNA Biology（增强子RNA生物学）

### 1.1 eRNA的产生

部分活跃增强子不仅能够结合TF（转录因子）及其他调控蛋白，还能招募RNAPII（RNA聚合酶II；RNA Polymerase II），在增强子附近启动转录。

典型的bidirectional enhancer transcription（双向增强子转录）：

`TF及辅因子招募 → RNAPII装载 → 双向转录起始 → 产生eRNAs`

- **Enhancer TSS（增强子转录起始位点）**：增强子中RNA转录开始的位置。
    
- **Divergent transcription（发散转录）**：转录从邻近起始位置向相反方向延伸。
    
- **μ（双向转录中心）**：根据新生转录信号计算推断的RNAPII装载及转录起始中心。
    

### 1.2 eRNA的主要类型

eRNA属于non-coding RNA（非编码RNA），但其结构与稳定性存在差异。

|特征|典型1D eRNA|典型2D eRNA|
|---|---|---|
|转录方向|单向|双向|
|长度|通常较长|通常较短|
|Splicing（剪接）|可以发生|多数未经剪接|
|Polyadenylation（多聚腺苷酸化）|可以具有poly(A) tail|多数不具有poly(A) tail|
|稳定性|部分较稳定|通常不稳定|

许多双向eRNA在转录后会被快速降解，因此普通poly(A)-selected RNA-seq可能无法充分捕获。

### 1.3 eRNA的三种不同生物学含义

|层次|研究对象|核心问题|
|---|---|---|
|Enhancer DNA|DNA调控序列|该序列能否调控基因表达？|
|Enhancer transcription|RNAPII介导的转录过程|转录活动本身是否参与调控？|
|eRNA molecule|转录产生的RNA分子|RNA分子是否具有独立功能？|

eRNA分子可能通过结合调控蛋白、影响转录复合物或染色质结构参与基因调控。

但是：

- eRNA表达与靶基因表达相关，不代表eRNA分子直接调控靶基因。
    
- 删除增强子DNA后基因表达改变，不足以证明RNA分子本身具有功能。
    
- 要区分RNA分子与转录过程的作用，需要能够分别扰动二者的实验设计。
    

**eRNA既可以作为enhancer activity的分子标记，也可能具有调控功能，但这两种角色需要分别验证。**

---

## 2. Nascent Transcription（新生转录）

### 2.1 RNA abundance与Transcriptional activity

细胞中检测到的RNA丰度不仅取决于合成速度，还取决于RNA降解速度。

简化表示：

`RNA abundance变化 = RNA synthesis − RNA degradation`

因此，成熟RNA的丰度并不总能直接反映当前的转录活性。

**Nascent RNA（新生RNA）**指正在由RNA聚合酶合成的RNA。

|方法|主要检测对象|
|---|---|
|常规RNA-seq|样本中积累的RNA|
|5′ scRNA-seq|捕获RNA 5′端信息，可用于定位转录起始事件|
|GRO-seq|正在延伸的RNA聚合酶产生的新生RNA|
|PRO-seq|高分辨率定位RNA聚合酶相关的新生转录|
|CAGE|利用加帽RNA的5′端定位转录起始位点|

### 2.2 Enhancer transcription与Gene transcription

同一次细胞刺激可能同时改变：

- Enhancer eRNA transcription。
    
- Target gene nascent transcription。
    
- Mature mRNA abundance。
    

但三者不一定同步，也不一定具有相同的变化幅度。

例如：

`刺激 → eRNA转录迅速升高 → 靶基因新生转录升高 → 成熟mRNA逐渐积累`

这只是一种可能的变化顺序。

**转录同步变化提供关联证据，而不是直接的调控因果证据。**

---

## 3. Genetic Variants & Disease Risk（遗传变异与疾病风险）

### 3.1 GWAS Signal与Functional Variant

GWAS（全基因组关联研究）通过比较genotype（基因型）与phenotype（表型），寻找具有统计关联的遗传位点。

需要区分：

- **Lead SNP（先导SNP）**：某个关联区域中统计信号最突出的代表性SNP。
    
- **Causal variant（因果变异）**：真正对相关生物学过程或表型产生因果影响的变异。
    
- **LD（连锁不平衡）**：不同遗传变异之间的非随机关联，使多个SNP可能共同出现关联信号。
    
- **Fine mapping（精细定位）**：利用遗传统计信息估计哪些变异更可能解释关联信号。
    

`GWAS association → LD / fine mapping → candidate causal variants → functional validation`

GWAS的显著性不等于功能效应的大小，也不等于因果证据的强弱。

### 3.2 Allele Frequency与Functional Effect

- **Major allele（主要等位基因）**：研究群体中较常见的等位基因。
    
- **Minor allele（次要等位基因）**：较少见的等位基因。
    
- **MAF（Minor Allele Frequency，次要等位基因频率）**：次要等位基因在群体中的频率。
    
- **Effect allele（效应等位基因）**：遗传统计模型中用于定义效应方向的等位基因。
    

Major/minor描述群体频率，不代表生物学功能的强弱。

例如，SNP改变某个TF motif中的关键碱基，可能导致TF结合倾向发生变化。

但motif prediction（基序预测）只能提出机制假设，需要功能实验验证。

### 3.3 Genetic Association与Molecular Mechanism

一个非编码SNP可能通过以下过程影响表型：

`SNP → TF结合或局部调控改变 → Enhancer activity变化 → Gene expression变化 → Cellular phenotype变化`

其中每个箭头都需要相应证据支持。

---

## 4. Environmental Signals & Asthma（环境信号与哮喘）

### 4.1 Airway Epithelium（气道上皮）

气道上皮细胞构成呼吸道的重要屏障，并参与识别环境刺激、产生炎症信号和调节局部免疫反应。

Asthma（哮喘）是一种异质性慢性气道疾病，常涉及：

- Airway inflammation（气道炎症）。
    
- Airway hyperresponsiveness（气道高反应性）。
    
- Variable airflow limitation（可变性气流受限）。
    
- Airway remodeling（气道重塑）。
    

BEAS-2B是永生化人支气管上皮细胞系，适合研究刺激诱导的转录调控，但不能完全代表患者体内的气道环境。

### 4.2 GR Signaling（糖皮质激素受体信号）

**NR3C1（核受体亚家族3 C组成员1；Nuclear Receptor Subfamily 3 Group C Member 1）**编码GR（糖皮质激素受体；Glucocorticoid Receptor）。

基本过程：

`Dex → GR激活 → 结合GRE或与其他调控蛋白相互作用 → 改变靶基因转录`

- **Dex（Dexamethasone，地塞米松）**：合成糖皮质激素。
    
- **GRE（Glucocorticoid Response Element，糖皮质激素响应元件）**：GR能够识别的DNA调控序列。
    
- **FKBP5（FK506结合蛋白5；FK506 Binding Protein 5）**：经典GR响应基因，也参与GR信号的反馈调节。
    

GR可以促进或抑制不同靶基因的转录，因此不能将GR激活简单理解为所有靶基因表达上升。

### 4.3 AHR Signaling（芳香烃受体信号）

**AHR（芳香烃受体；Aryl Hydrocarbon Receptor）**是一种配体激活型转录因子，能够响应多种内源性及环境来源的小分子化合物。

典型过程：

`AHR ligand → AHR激活 → 与ARNT形成复合物 → 结合AHR response element → 调节基因转录`

- **ARNT（芳香烃受体核转位蛋白；Aryl Hydrocarbon Receptor Nuclear Translocator）**：AHR的转录调控伙伴。
    
- **AHRE/XRE（AHR/Xenobiotic Response Element，芳香烃受体/外源性物质响应元件）**：AHR复合物识别的DNA序列。
    
- **TCDD**：强效AHR激动剂，常用于研究AHR相关机制。
    
- **WSP（Wood Smoke Particles，木材烟雾颗粒物）**：复杂环境污染物混合物，部分成分可激活AHR。
    

AHR具有环境感知、代谢调控和免疫调节等多种作用，不应简单归类为促炎或抗炎因子。

### 4.4 AHR–GR Cross-talk（信号交叉调控）

AHR与GR可以在多个层面发生交叉调控：

- 改变转录因子及其辅因子的活性。
    
- 调节共同的下游基因。
    
- 影响彼此相关的转录调控网络。
    
- 在特定环境下影响NR3C1及GR相关转录响应。
    

因此，环境污染物可能改变细胞对糖皮质激素的转录响应。

但具体变化方向取决于刺激、细胞类型及调控环境。

**Sasse 2025：环境暴露相关信号可能通过遗传变异敏感的增强子，与气道炎症和糖皮质激素响应产生联系。**

---

## 5. Genetic Regulation of eRNA Expression（eRNA表达的遗传调控）

### 5.1 eQTL与eRNA eQTL

eQTL（Expression Quantitative Trait Locus，表达数量性状位点）指与RNA表达水平存在统计关联的遗传变异。

例如：

某个SNP具有C/T两种等位基因。

如果在同一种组织中，携带不同等位基因的个体具有不同的RNA表达水平，就可能检测到eQTL。

|类型|研究的表达性状|
|---|---|
|Gene eQTL|基因RNA表达量|
|eRNA eQTL|增强子RNA表达量|

eQTL通常还区分：

- **cis-eQTL（顺式eQTL）**：研究位点附近的遗传变异与表达之间的关联。
    
- **trans-eQTL（反式eQTL）**：研究相距较远、甚至不同染色体上的遗传关联。
    

一个SNP可能同时与eRNA和邻近基因的表达相关，但这不意味着eRNA分子必然介导了该SNP对基因的影响。

### 5.2 GReX（遗传调控表达量）

GReX，全称Genetically Regulated Expression（遗传调控的表达成分）。

表达量可以受到多种因素影响：

`Observed expression = Genetic contribution + Environmental / cellular contribution + Other variation`

GReX模型利用遗传变异预测RNA表达中的遗传相关成分。

例如：

`SNP genotypes → Expression prediction model → Predicted eRNA expression`

它与直接测量的RNA expression不同：

- Observed expression：实际测量的RNA水平。
    
- GReX：依据基因型估计的遗传调控表达成分。
    

因此，GReX并不包含所有环境因素、细胞状态及随机转录波动的影响。

### 5.3 Tissue-specific Genetic Regulation（组织特异性遗传调控）

同一个SNP对RNA表达的影响可能因组织而异。

例如：

- SNP-A在脑组织中影响某个eRNA表达。
    
- 同一SNP在血液中可能没有可检测的表达效应。
    

原因包括不同组织具有不同的TF、染色质状态及调控环境。

因此，eRNA eQTL与GReX分析需要考虑tissue specificity（组织特异性）。

---

## 6. eRNA, Chromatin Contacts & Disease Genetics

### 6.1 Chromatin Contact Frequency（染色质接触频率）

染色质接触频率描述两个基因组区域在群体测序实验中被检测为相互接触的相对频繁程度。

需要区分：

- **Genomic distance（基因组线性距离）**：两个DNA位点沿染色体相隔多少bp。
    
- **Chromatin contact frequency（染色质接触频率）**：二者在三维染色质中被检测到的相对接触信号。
    
- **Functional regulatory interaction（功能性调控互作）**：一个区域确实影响另一个区域的调控活动。
    

接触频率受线性距离、染色质结构、细胞状态及实验测量因素影响。

`eRNA expression能够预测chromatin contact ≠ eRNA分子直接促成chromatin contact`

### 6.2 eRNA参与调控的潜在机制

已有研究提出几类可能的eRNA作用机制：

|机制|可能的分子过程|
|---|---|
|Contact-dependent|eRNA与cohesin等蛋白相互作用，参与维持或促进特定染色质接触|
|Contact-independent|eRNA结合TF或染色质调控蛋白，影响局部转录环境|
|Transcription-associated|增强子转录过程本身参与改变局部调控状态|

其中：

- **Cohesin（黏连蛋白复合物）**：参与染色质环形成和维持。
    
- **CBP/p300**：具有组蛋白乙酰转移酶活性的转录共激活因子。
    
- **YY1（Yin Yang 1，阴阳蛋白1）**：参与多种转录调控及部分染色质互作过程的转录因子。
    

这些是可能的机制类别，并非所有eRNA都通过相同方式发挥作用。

### 6.3 TWAS（转录组关联研究）

TWAS，全称Transcriptome-Wide Association Study（转录组范围关联研究）。

它通过遗传预测的RNA表达与疾病GWAS信息，检验基因表达相关遗传成分是否与疾病性状存在关联。

简化流程：

`Genotype → Predicted expression (GReX) → Trait association`

与GWAS相比：

- GWAS主要研究SNP与表型的关联。
    
- TWAS主要研究遗传预测的表达与表型的关联。
    

如果将传统gene expression替换为eRNA expression，就可以开展eRNA-based TWAS。

**TWAS显著不代表RNA表达变化已经被证明导致疾病。** 结果可能受到LD及不同表达性状共享遗传信号的影响。

### 6.4 Colocalization（共定位分析）

Colocalization用于判断：

**两个关联信号是否可能由同一个遗传变异驱动？**

例如，在同一基因组区域发现：

- 一个SNP与eRNA表达相关（eQTL）。
    
- 一个SNP与疾病相关（GWAS）。
    

共定位分析可以比较两种解释：

1. eRNA eQTL与疾病GWAS可能共享因果变异。
    
2. 两种信号可能来自不同但存在LD的变异。
    

如果支持共享变异，就增加了该调控区域与疾病之间存在共同遗传基础的证据。

但共定位仍不能证明：

`eRNA molecule → Disease`

因为共享遗传信号可能通过其他分子机制发挥作用。

### 6.5 Mendelian Randomization（孟德尔随机化）

MR利用与某种exposure（暴露或待研究性状）相关的遗传变异，推断该性状对outcome（结局）的潜在因果效应。

例如：

`Genetic variant → eRNA expression → Disease risk`

这里eRNA expression是exposure，疾病风险是outcome。

MR需要满足重要假设：

- 遗传工具变量与exposure有关。
    
- 工具变量与exposure–outcome关系的混杂因素独立。
    
- 工具变量不会通过exposure以外的途径影响outcome。

---

## 7. Transposable Elements & Enhancer Evolution（转座元件与增强子演化）

TEs（Transposable Elements，转座元件）是能够通过不同机制在基因组中移动或复制的DNA序列。

主要类别包括：

|类型|含义|
|---|---|
|LTR retrotransposons|具有长末端重复序列的反转录转座元件|
|LINE|Long Interspersed Nuclear Elements，长散在核元件|
|SINE|Short Interspersed Nuclear Elements，短散在核元件|
|DNA transposons|DNA转座元件|

TE序列在演化过程中可能提供新的TF binding motifs、转录起始位点或调控序列，从而被细胞调控网络利用。

因此，部分细胞状态特异性增强子可能来源于或重叠于TE序列。

**TE与活性增强子重叠，不代表TE本身必然具有增强子功能，也不代表其来源决定了当前的调控活性。**

---

## 8. Three Papers — Biological Connections

|论文|生物学核心|关键新增知识|
|---|---|---|
|**Oguchi 2024**|eRNA transcription与细胞身份及免疫疾病遗传学|双向转录、增强子TSS、细胞状态特异性、TE来源|
|**Sasse 2025**|遗传变异与环境刺激响应|SNP等位基因效应、GR/AHR信号、气道炎症|
|**Betti 2025**|eRNA表达的遗传调控与复杂疾病|eRNA eQTL、GReX、TWAS、MR、colocalization|

### Core Takeaways

1. eRNA transcription是研究活性增强子的重要信号，但不能直接代表eRNA分子的功能。
    
2. 非编码SNP可以改变调控DNA的功能，进而影响基因表达；GWAS关联与分子功能因果关系需要分别验证。
    
3. eRNA表达也可能受到遗传变异调控，并提供传统基因表达分析之外的遗传学信息。
    
4. 预测、遗传共定位、统计因果推断与实验功能验证提供不同类型的证据，不能相互替代。
    