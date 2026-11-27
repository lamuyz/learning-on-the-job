# ReapTEC: Methodology & Benchmark

**Oguchi et al., Science, 2024**

_An atlas of transcribed enhancers across helper T cell diversity for decoding human diseases_

[DOI: 10.1126/science.add8394](https://doi.org/10.1126/science.add8394) | [GitHub: ReapTEC](https://github.com/MurakawaLab/ReapTEC)

## 01. Methodology

### 1.1 Read-level prefiltering

ReapTEC（Read-level prefiltering and transcribed enhancer call）利用5′ scRNA-seq 数据识别 TSS，并根据背向双向转录特征识别 btcEnhs（Bidirectionally transcribed candidate enhancers，双向转录候选增强子）。

普通5′ scRNA-seq 数据中，由于 strand invasion（链侵入）和 premature template switching（提前模板转换）等因素，reads 的5′端不一定对应真实的转录起始位置。

RNA 的5′ cap 在逆转录过程中可以产生额外的 C，对应到 RNA 正义方向的测序序列中就是额外的 G。这个 G 不是由对应的参考基因组序列直接编码的，因此比对时可能表现为 soft-clipped G。

作者将 R1 延长至150 bp，以获得 RNA 的5′端序列。

|R1 位置|内容|
|---|---|
|1–16 bp|Cell barcode|
|17–26 bp|UMI|
|27–39 bp|TSO 相关序列|
|40 bp 及之后|RNA 来源序列及可能存在的额外 G|

通过 STARsolo 进行序列比对，再根据 BAM 文件中的 CIGAR 和 SEQ 信息进行筛选。

源代码中的正链筛选条件：

- CIGAR：`^40S[0-9]`
    
- SEQ：第40位为 G
    

负链比对记录则根据反向互补关系检查对应的 C。

**为什么不直接使用所有 reads？**

因为有些 reads 的5′端可能来自 RNA 内部，而不是真实的 TSS。通过额外 G 筛选可以减少这部分背景信号。

但如果额外 G 恰好能够与参考基因组匹配，或者真实的5′端没有产生额外 G，那么这些真实信号也可能被过滤掉。

所以这里其实存在一个问题：额外 G 筛选在减少噪声的同时，会损失多少真实的转录起始信号？

### 1.2 Workflow

FASTQ → STARsolo → BAM → Read-level filtering → UMI deduplication → CTSS → TSS peaks → btcEnhs

CTSS（CAGE Tag Starting Site）是根据测序数据推断得到的单碱基转录起始信号。

使用 `bedtools merge -d 10 -s` 将距离较近、方向相同的 CTSS 合并为 TSS peaks。

Peak calling 和 Quantification 是两个不同的过程。前者是确定需要研究的基因组区域，后者是统计这些区域中的转录信号。

不同细胞产生的 CTSS 可以共同参与 peak calling，确定 peak 坐标后，再根据原始 CTSS 文件中的 cell barcode 和 count 信息进行定量。

### 1.3 Enhancer calling

ReapTEC 主要识别具有 Divergent transcription（背向双向转录）特征的候选增强子。

```
负链转录 ←—— Enhancer ——→ 正链转录
```

主要筛选条件：

|条件|作用|
|---|---|
|异链 peak 配对|负链 peak 在左，正链 peak 在右|
|Peaks 不重叠|排除发生重叠的异链 peak 配对|
|DIST = 400 bp|限制异链 peaks 的配对距离|
|WIN = 200 bp|候选区域中心左右各设置一个定量窗口|
|Promoter masking|排除与蛋白编码转录本 TSS ±300 bp 重叠的候选区域|
|左侧正链/负链 < 1|左侧以向外的负链转录为主|
|右侧负链/正链 < 1|右侧以向外的正链转录为主|
|\|D\| < 0.8|排除双向转录过于失衡的区域|
|Exonic filtering|排除位于外显子且不与 CD4⁺ T 细胞 DHS 重叠的候选区域|

Directionality score：

D = (F − R) / (F + R)

F 和 R 分别表示预期向外转录的正链和负链信号。D 越接近0，双向转录越平衡。

候选区域需要在至少一个输入样本中满足相应的双向转录条件，而不是要求每个细胞都存在双向转录信号。

**已经将 CTSS 合并成 peaks 了，为什么还要设置左右各200 bp的窗口？**

这两个操作的目的不一样。Peak calling 是为了确定转录起始区域，而设置窗口是为了统计候选区域两侧的转录信号，判断是否符合增强子的双向转录特征，并不是再次合并 CTSS。

另外，正负链 peaks 发生重叠或者双向转录不平衡，并不代表这个区域一定不是增强子。这些条件实际上是 ReapTEC 对 btcEnh 的定义。

所以后续比较不同工具时，需要注意识别结果的差异是否仅仅来自工具对增强子的定义不同。

_具体距离参数及区间边界需要结合原文方法和相应版本的源代码确认。_

## 02. Method Validation

作者先验证额外 G 是否能够作为可靠的筛选依据，再验证这种筛选方式在真实数据中的效果，最后评价识别出的候选增强子是否具有相应的生物学特征。

### 2.1 额外 G 筛选的可靠性（Figure S2C–D）

作者使用人工合成的戴帽 ERCC RNA 测序数据，比较 cap-trapper、template switching 和 oligo-capping 等方法获得的 reads。

使用 ERCC 的好处是，它的真实5′端位置是已知的，可以作为 Ground truth。

根据 reads 的比对位置，将其分为真实5′端信号和 RNA 内部背景信号，再统计两类 reads 中额外 G 的分布。

结果发现，在逆转录时保留帽结构的方法中，来自真实5′端的 reads 通常具有额外 G，而 RNA 内部的背景信号通常没有这一特征。

这里并不是通过额外 G 判断哪些 reads 来自真实 TSS，而是先根据 ERCC 已知的5′端确定真实信号，再反过来验证额外 G 这个特征是否可靠。

这种使用已知真实答案的数据进行验证的方式，后续做 TSS identification benchmark 时可以参考。

### 2.2 真实数据中的筛选效果（Figure 1E–F）

作者在 CD4⁺ T 细胞5′ scRNA-seq 数据中比较了三种 reads 筛选策略。

|筛选策略|TSS region mapping proportion|
|---|---|
|All reads|82.1%|
|G-start reads|88.3%|
|Unencoded G reads|98.1%|

为什么要单独设置 G-start 这一组？

因为作者不仅需要证明筛选后信号质量有所提高，还需要说明真正有价值的是 unencoded G 这个特征，而不只是 reads 以 G 开头。

这里的 TSS region 是 GENCODE v39 注释的转录本5′端 ±300 bp。只要 read 的5′端落在这个约600 bp的区域内，就归入 TSS region。

因此，98.1%不能直接理解为 TSS 识别准确率：

- 落在±300 bp内不代表准确定位到了真实的转录起始碱基。
    
- 落在区域之外也可能是真实的 eRNA 或未注释 RNA。
    
- 这个比例没有告诉我们过滤过程中损失了多少真实信号。
    

Figure 1E 是全局统计，Figure 1F 则通过 SOCS7 基因附近的实际案例，进一步展示不同筛选策略对背景信号的影响。

后续如果评价类似的过滤策略，除了统计过滤后信号的质量，应该也需要关注真实信号的保留情况。

### 2.3 eRNA 定量验证（Figure 1G）

作者比较了12,433个由 CAGE 和 NET-CAGE 定义的增强子区域在两种数据中的转录水平：

- Pseudobulk 5′ scRNA-seq
    
- NET-CAGE
    

相关系数 r = 0.67。

CAGE（Cap Analysis of Gene Expression）主要用于检测戴帽 RNA 的5′端，NET-CAGE 则用于检测新生 RNA 的转录起始信号。

使用 NET-CAGE 相当于利用另一种实验技术获得的测量结果，评价5′ scRNA-seq 对 eRNA 转录水平的定量能力，即 Orthogonal validation（正交验证）。

但这里的增强子区域是提前定义好的，所以作者验证的是两种技术对相同区域的定量结果是否一致，而不是 ReapTEC 能否准确识别出这些增强子。

另外，这里使用的是 Pseudobulk 数据，不能直接说明单细胞层面的定量准确性。

### 2.4 Internal priming（Figure S3）

eRNA 通常不具有 poly(A) 尾，但是 oligo(dT) 可以结合 RNA 内部的 A-rich region（富 A 区域）并启动逆转录，即 Internal priming（内部引物引发）。

作者使用 MAS-seq 长读长测序分析 cDNA 比对末端附近的基因组序列。

|图号|分析内容|
|---|---|
|S3A–B|长读长测序数据的长度及质量|
|S3C|具体区域中 cDNA 末端附近的富 A/T 序列|
|S3D|全局统计比对末端附近的碱基频率|

正链表现为 A 富集，负链表现为 T 富集，实际上对应的都是 RNA 中的富 A 序列。

因为 ReapTEC 关注的是转录起始位置，所以即使 Internal priming 导致部分 RNA 序列没有被逆转录，只要逆转录到达真实5′端，就仍然可以利用这部分信号。

但是，如果某些 eRNA 内部没有适合 oligo(dT) 结合的区域，那么这些 eRNA 可能从建库阶段就没有被有效捕获。

所以没有识别出某个增强子，不一定是计算工具的问题，也可能是实验技术本身的限制。这一点在后续评价工具的灵敏度时需要考虑。

### 2.5 表观遗传验证（Figure 1I）

作者比较使用与不使用 ReapTEC 过滤时，识别出的候选增强子周围的表观遗传信号。

|信号|生物学意义|
|---|---|
|DHS|染色质可及性|
|H3K27ac|活跃调控区域相关修饰|
|H3K4me1|增强子相关组蛋白修饰|

使用 ReapTEC 过滤后，候选增强子与上述表观遗传特征的一致性更高。

这种设计类似于 Ablation study（消融实验），即通过改变某个关键步骤，观察它对最终识别结果的影响。

**Metagene analysis（聚合信号分析）**

这个画图方法以后应该可以用得上。

基本流程：

1. 获得候选增强子的 BED 文件。
    
2. 以每个增强子的中心为参考点，向两侧各延伸2 kb。
    
3. 从外部 bigWig 文件中提取相应区域的信号。
    
4. 将所有候选增强子按照中心位置对齐，绘制热图或聚合信号曲线。
    

相关工具：deepTools。

```
computeMatrix reference-point \
    --referencePoint center \
    -S signal.bw \
    -R enhancers.bed \
    -a 2000 -b 2000 \
    -bs 10 \
    -o matrix.gz
```

再使用 `plotHeatmap` 或 `plotProfile` 进行可视化。

以上为分析命令模板。

这里有一个我还没有完全理解的问题：作者识别的是 Treg cluster 11 中的候选增强子，但是用于验证的是 ENCODE CD4⁺ T 细胞的表观遗传数据。不同细胞群的增强子活性不是可能存在差异吗？

目前的理解是，这种比较能够说明候选增强子所在的基因组区域整体具有相应的表观遗传特征，但不能证明这些特征一定存在于原来的 Treg 细胞群中。

如果后续做类似的验证，应该尽量选择细胞类型匹配的外部数据。

另外，ReapTEC 本身使用了 DHS 对部分外显子候选增强子进行过滤，因此 DHS 不能完全作为独立的验证证据。

## 03. Benchmark & Evaluation

### 3.1 ReapTEC vs. SCAFE（Figure S4）

两种工具都利用5′ scRNA-seq 数据识别转录起始区域及相关调控元件，主要区别之一在于背景信号的处理阶段。

| Feature | ReapTEC | SCAFE |
| --- | --- | --- |
| 关键过滤阶段 | Read level | Peak level |
| 主要过滤策略 | Unencoded G | 逻辑回归分类器 |
| 主要输出 | btcEnhs | tCREs |

tCREs：Transcribed cis-Regulatory Elements（发生转录的顺式调控元件）。

#### Figure S4A：Directionality

SCAFE 识别出的远端 tCREs 包括：

- Unidirectional：68%
    
- Convergent：8%
    
- Bidirectional：24%
    

S4A 其实是在为后面的工具比较做准备，因为 SCAFE 识别出的区域不全是背向双向转录区域，而 ReapTEC 主要识别具有这一特征的候选增强子。

所以不能直接比较两个工具识别出的全部区域数量，应该先确定两者识别的是不是同一种东西。

#### Figure S4B：Number of calls

ReapTEC 识别出的双向转录区域更多。

但是识别数量更多是否就意味着工具的灵敏度更高？

如果新增区域是真实的增强子，那么可以说明工具具有更好的检测能力；如果新增区域中包含大量假阳性，那么识别数量更多并不是优势。

因此还需要结合其他实验数据进行验证。

#### Figure S4C：Region length

| Tool    | Median region length |
| ------- | -------------------- |
| ReapTEC | 202 bp               |
| SCAFE   | 501 bp               |

区域长度更短，主要是因为它可以帮助我们缩小增强子及其相关 TSS 的研究范围。例如后续寻找 TF binding motifs 或定位 SNP 时，可以将分析范围缩小到更具体的区域。

但是怎么知道缩小后的范围就是更加准确的？

目前 S4C 只能说明 ReapTEC 识别的区间整体更窄。在缺乏真实增强子边界的情况下，不能直接证明其定位误差更小。

#### Figure S4D：Expression distribution

作者比较两种工具识别区域的表达水平分布，发现 ReapTEC 能够识别较多低表达区域。

由于 eRNA 通常表达量较低，这应该是评价工具性能时需要重点关注的内容。

不过，S4B–C 比较的是两个工具的双向转录区域，而 S4D 比较的是 ReapTEC 的 btcEnhs 和 SCAFE 的全部远端 tCREs。

这里的比较口径并不完全一致。

后续做类似的 Benchmark 时，除了统一候选区域的定义，应该还需要统一表达定量及归一化方法，否则表达分布的差异不一定完全来自工具的检测能力。

#### Figure S4E：Genome browser visualization

通过具体的基因组区域进一步说明 S4B–D 中观察到的差异。

例如在同一个区域，ReapTEC 和 SCAFE 都识别出了候选调控元件，但 ReapTEC 定义的区域更窄，并且更加集中于双向转录起始信号附近。

S4C 是从全局统计角度说明区间长度的差异，S4E 则是展示具体区域中这种差异是怎样产生的。

这个图以后应该也可以用得上。

除了比较不同工具识别出的增强子数量，还可以挑选一些具体区域，看看为什么一个工具识别出来了，而另一个没有。是原始信号的问题、read filtering 的差异，还是 peak calling 和 enhancer calling 的条件不同？

### 3.2 增强子图谱的整体评价（Figure 2E、S11A–B）

作者对136个 CD4⁺ T 细胞 clusters 分别运行 ReapTEC，最终构建了包含62,803个 btcEnhs 的增强子图谱。

Figure 2E 使用与 Figure 1I 类似的热图，观察整个图谱中候选增强子周围的表观遗传信号。

Figure S11 则进一步评价这些区域与已有调控元件数据库之间的关系。

#### Figure S11A：Enrichment analysis

作者比较 btcEnhs 与随机基因组区域在 ENCODE cCREs（Candidate cis-Regulatory Elements，候选顺式调控元件）中的富集程度。

|ENCODE cCREs|含义|
|---|---|
|dELS|远端增强子样特征|
|pELS|近端增强子样特征|
|PLS|启动子样特征|
|DNase|DNase I 高敏感相关类别|
|CTCF-only|仅具有 CTCF 相关特征的类别|

为什么还需要随机对照？

假设一个工具识别出的候选增强子中有60%与 ENCODE dELS 重叠，但是如果随机选择的基因组区域也有60%与 dELS 重叠，那么这个结果其实没有太大的说服力。

作者使用与 btcEnhs 具有相同长度分布的随机区域作为对照。

保持长度分布一致是因为区域越长，通常越容易与其他区域发生重叠。

Fold enrichment（富集倍数）的基本计算思路：

实际重叠比例 / 随机背景重叠比例

相关工具：`bedtools shuffle`、`bedtools intersect`。

不同工具识别出的区域长度可能存在较大差异，例如 ReapTEC 和 SCAFE。因此，后续进行数据库重叠分析时，除了直接比较重叠比例，也可以考虑使用匹配的随机背景进行富集分析。

#### Figure S11B：Overlap analysis

约66%的 btcEnhs 与 ENCODE cCREs 重叠，约34%未发生重叠。

Overlap analysis 和 Enrichment analysis 回答的问题其实不一样：

- Overlap：有多少候选区域获得了已有数据库的支持？
    
- Enrichment：相比随机背景，这些候选区域是否更倾向于分布在具有调控特征的基因组位置？
    

这里还有一个问题：未与 ENCODE cCREs 重叠的34%候选区域，到底是新发现的增强子，还是工具产生的假阳性？

已有数据库不可能包含所有真实增强子，因此不能直接将数据库重叠比例当作工具的 Precision。

作者在 Figure S11C–F 中对这部分问题进行了进一步分析（待阅读）。

### 3.3 后续 Benchmark 可以参考的评价方法

|评价维度|分析方法|原文|
|---|---|---|
|TSS identification|已知起始位置验证、TSS 区域比对比例|S2、1E|
|Noise reduction|不同过滤策略的比较|1E–F|
|Quantification|与 NET-CAGE 的表达相关性|1G|
|Detection capability|识别数量及表达水平分布|S4B、D|
|Spatial resolution|区域长度分布|S4C|
|Epigenetic support|DHS、H3K27ac、H3K4me1 聚合信号|1I、2E|
|Database consistency|重叠分析及随机背景富集分析|S11A–B|
|Case study|Genome browser 可视化|1F、S4E|

Figure S4 主要比较了识别数量、区域长度和低表达信号的检测情况，并没有直接评价 Precision、Recall、F1 score、Runtime、Memory usage，以及不同测序深度下的稳健性。

后续可以结合实际研究目的，考虑是否需要补充这些评价指标。

## 04. Discussion

### 4.1 如何区分实验技术限制和计算工具限制？

假设 NET-CAGE 检测到了某个增强子的转录信号，但是 ReapTEC 没有识别出该区域，应该怎么判断问题出在哪里？

可以沿着整个计算流程检查中间结果。

|检查阶段|可能的原因|
|---|---|
|原始 reads / BAM|RNA 未被捕获、测序深度不足或比对失败|
|Filtered CTSS|不符合额外 G 筛选条件|
|TSS peaks|信号不足以形成有效 peak|
|btcEnhs|不满足双向转录、配对距离或方向性等筛选条件|

如果原始数据已经存在相关信号，但是在某一个计算步骤之后消失，就可以进一步检查这个步骤的筛选条件。

如果原始数据中就不存在有效信号，那么可能是实验捕获、测序深度或比对的问题，但仅凭这些结果还不能确定是哪一种。

后续比较不同工具时，可以考虑使用相同 FASTQ、比较中间文件，以及通过 Downsampling 评价不同测序深度下的表现。

我觉得除了比较最终识别结果，还需要进一步分析差异是在哪一步产生的，这样才能更好地理解不同工具的优势和局限。

### 4.2 Open questions

- 额外 G 筛选在减少背景信号的同时，会损失多少真实 TSS 信号？应该如何评价这种 trade-off？
    
- 如果不同工具对候选增强子的定义、区域长度及筛选条件不完全一致，应该怎样公平地进行比较？
    
- 如果没有完整的真实增强子参考集合，应该如何计算 Precision 和 Recall？
    
- 如果新方法额外识别出了大量低表达、未被已有数据库注释的候选增强子，应该利用哪些独立证据判断它们是否真实？
    

## Tools & Resources

|Tool|Application|
|---|---|
|STARsolo|序列比对及单细胞信息处理|
|SAMtools|BAM 文件处理|
|UMI-tools|UMI 去重|
|bedtools merge|合并相邻基因组区域|
|bedtools intersect|基因组区域重叠分析|
|bedtools shuffle|构建随机对照区域|
|deepTools|表观遗传信号提取及可视化|
|UCSC Genome Browser|具体基因组区域中的信号展示|

[ReapTEC](https://github.com/MurakawaLab/ReapTEC) | [ENCODE](https://www.encodeproject.org/) | [GENCODE](https://www.gencodegenes.org/) | [FANTOM5](https://fantom.gsc.riken.jp/5/) | [BEDTools](https://bedtools.readthedocs.io/) | [deepTools](https://deeptools.readthedocs.io/)

## Further Reading

- Fig. S11C–F：新发现的候选增强子的可靠性及功能验证（MPRA）。
    
- Fig. 2F–J：eRNA 转录与染色质可及性的关系。
    
- Fig. S14：TSS-level expression matrix、robust TSS peaks 及细胞聚类。