# T Cell Atlas ：生物学背景知识

## 1. 阅读文献与整体框架

### 1.1 阅读文献

1. Zheng et al., *Science*, 2021  
   *Pan-cancer single-cell landscape of tumor-infiltrating T cells*

2. Chu et al., *Nature Medicine*, 2023  
   *Pan-cancer T cell atlas links a cellular stress response state to immunotherapy resistance*

3. Liu et al., *Cell*, 2025  
   *A single-cell atlas reveals immune heterogeneity in anti-PD-1-treated non-small cell lung cancer*

### 1.2 三篇论文的研究逻辑

- **Zheng 2021**：识别肿瘤浸润T细胞的类型、状态、分化关系及跨癌种异质性。
- **Chu 2023**：研究T细胞应激反应状态及其与免疫治疗抵抗的关系。
- **Liu 2025**：研究肿瘤免疫微环境的异质性及其与治疗应答、患者预后的关系。

共同的生物学主线：

```text
肿瘤抗原识别与T细胞激活
           ↓
      T细胞增殖与分化
           ↓
      形成不同功能状态
           ↓
    耗竭 / 应激 / 免疫调节
           ↓
 与其他免疫细胞共同构成TIME
           ↓
      影响抗肿瘤免疫
           ↓
   与免疫治疗应答和预后相关
```

---

## 2. T细胞的抗原识别与激活

### 2.1 肿瘤免疫的基本过程

正常情况下，免疫系统能够识别并清除部分异常细胞，其中T细胞是抗肿瘤适应性免疫的重要组成部分。

```text
肿瘤细胞产生异常抗原
          ↓
抗原呈递细胞摄取、加工并呈递抗原
          ↓
      初始T细胞激活
          ↓
      T细胞增殖与分化
          ↓
   效应T细胞进入肿瘤组织
          ↓
    识别并攻击肿瘤细胞
```

但肿瘤可能通过抗原呈递缺陷、免疫抑制性信号、代谢竞争和免疫抑制性细胞等机制逃避免疫攻击。

### 2.2 TCR–MHC抗原识别

核心概念：

- **Antigen（抗原）**：能够被免疫系统识别的分子或分子结构。
- **Neoantigen（新抗原）**：通常由肿瘤体细胞突变产生、可能被免疫系统识别的新抗原。
- **TCR（T cell receptor，T细胞受体）**：识别特定抗原肽与MHC形成的复合物。
- **MHC（Major histocompatibility complex，主要组织相容性复合体）**：负责呈递抗原肽；在人类对应HLA分子系统。

常规αβ T细胞的TCR通常识别抗原肽–MHC复合物，而不是完整的游离抗原。

### 2.3 CD8⁺与CD4⁺ T细胞

| 特征 | CD8⁺ T cell | CD4⁺ T cell |
|---|---|---|
| 抗原识别 | Peptide–MHC-I | Peptide–MHC-II |
| 主要功能 | 直接杀伤靶细胞 | 协调、辅助或抑制免疫反应 |
| 常见亚群 | Effector、Memory、Trm、Tex | Th1、Th17、Tfh、Treg |
| 抗肿瘤作用 | 主要发挥细胞毒性作用 | 调节抗肿瘤免疫 |

需要注意：

- CD8⁺ T细胞并非只有杀伤功能。
- 部分CD4⁺ T细胞也具有细胞毒性。
- 两者具有不同的主要分化与功能程序，因此T cell atlas通常分别研究CD8⁺和CD4⁺ T细胞。

### 2.4 T细胞激活的三个信号

经典初始T细胞激活涉及三个信号：

1. **Signal 1（抗原识别）**：TCR识别抗原肽–MHC复合物。
2. **Signal 2（共刺激信号）**：例如CD28与CD80/CD86结合。
3. **Signal 3（细胞因子信号）**：如IL-2（Interleukin-2，白细胞介素2），调节T细胞增殖和分化。

因此，T细胞的最终状态不仅取决于抗原识别，也受到共刺激、细胞因子及微环境影响。

---

## 3. T细胞的分化与功能状态

### 3.1 主要T细胞亚群

| 亚群 | 主要功能 | 常见相关基因 |
|---|---|---|
| Naive T（初始T细胞） | 尚未经历相应抗原驱动的充分激活 | CCR7、SELL、TCF7 |
| Effector T（效应T细胞） | 杀伤靶细胞或分泌效应性细胞因子 | GZMB、PRF1、IFNG |
| Memory T（记忆T细胞） | 维持长期免疫反应 | IL7R、TCF7 |
| Trm（组织驻留记忆T细胞） | 长期驻留特定组织 | CD69、ITGAE、ZNF683 |
| Tex（耗竭T细胞） | 慢性抗原刺激相关的功能和分化重塑 | PDCD1、TOX、HAVCR2 |
| Treg（调节性T细胞） | 维持免疫耐受、抑制过度免疫反应 | FOXP3、IL2RA、CTLA4 |
| Tfh（滤泡辅助性T细胞） | 协助B细胞反应 | CXCR5、BCL6、IL21 |

这些基因是常见的细胞注释依据，但单个marker gene（标记基因）通常不足以唯一确定一个细胞亚群。

### 3.2 Cell type与Cell state

- **Cell type（细胞类型）**：具有相对稳定的谱系身份及功能特征的细胞类别。
- **Cell state（细胞状态）**：细胞在激活、分化、应激或环境刺激下表现出的功能与转录状态。
- **Transcriptional program（转录程序）**：一组具有共同生物学功能或调控关系的基因表达活动。

例如：

- Treg是具有特定免疫调节功能的T细胞群体。
- Tex强调慢性抗原刺激相关的耗竭分化状态。
- Stress-response program（应激反应程序）可以出现在不同T细胞亚群中。

**不同细胞共享某些转录特征，并不意味着它们具有相同的分化来源。**

例如，Zheng 2021中Terminal Tex表现出部分Treg-like features（Treg样特征），但不能据此推断Terminal Tex来源于Treg。

---

## 4. T Cell Exhaustion（T细胞耗竭）

### 4.1 耗竭如何产生？

持续抗原刺激（如慢性感染或肿瘤抗原）可能促使T细胞形成耗竭相关分化程序。

典型特征包括：

- 部分效应功能降低。
- 持续增殖能力发生变化。
- PD-1、TIM-3、LAG-3等抑制性受体表达增加。
- TOX等转录调控因子参与耗竭程序的建立和维持。
- 转录组与表观遗传状态发生重塑。

**耗竭并不意味着T细胞完全失去杀伤能力。**

### 4.2 Tpex与Terminal Tex

典型的简化分化框架：

```text
持续抗原刺激
      ↓
Tpex（前体耗竭T细胞）
      ↓
Intermediate Tex（中间耗竭态）
      ↓
Terminal Tex（终末耗竭态）
```

这不是所有肿瘤T细胞都必须遵循的单一、不可逆路径。

| 特征 | Tpex | Terminal Tex |
|---|---|---|
| 分化状态 | 前体样 | 终末分化样 |
| 自我更新潜能 | 相对较强 | 相对较弱 |
| 增殖潜能 | 通常较强 | 持续增殖潜能通常较低 |
| 相关基因 | TCF7、PDCD1等 | HAVCR2、TOX、PDCD1等 |
| ICB治疗反应 | 常是治疗后增殖反应的重要细胞来源 | 持续增殖反应通常较有限 |

**TCF7（Transcription factor 7，转录因子7）**编码TCF1蛋白，与部分前体样T细胞的维持有关。

注意：TCF7也可能在Naive T和Memory T中表达，因此不能单独作为Tpex的唯一判定依据。

---

## 5. T Cell Stress Response（T细胞应激反应）

### 5.1 什么是细胞应激？

T细胞进入肿瘤微环境后，可能面临：

- Hypoxia（缺氧）
- Nutrient limitation（营养限制）
- Oxidative stress（氧化应激）
- Proteotoxic stress（蛋白质稳态压力）

细胞会通过特定的应激反应程序维持生存和细胞稳态。

Heat shock response（热休克反应）是其中一种，与HSP（Heat shock proteins，热休克蛋白）有关。

常见相关基因：

- **HSPA1A**：Heat shock protein family A member 1A（热休克蛋白家族A成员1A）
- **HSP90AA1**：Heat shock protein 90 alpha family class A member 1（热休克蛋白90α家族A类成员1）
- **HSPD1**：Heat shock protein family D member 1（热休克蛋白家族D成员1）

这些蛋白参与蛋白质折叠、稳定性和应激适应。

### 5.2 T_STR与Tex的区别

Chu 2023识别了T_STR（stress-response T cells，应激反应T细胞），其特征是富集应激相关基因表达程序。

| 特征 | Tex | T_STR |
|---|---|---|
| 主要特点 | 耗竭相关分化程序 | 应激相关转录程序 |
| 相关刺激 | 持续抗原刺激 | 细胞内外环境压力 |
| 常见分子特征 | PDCD1、TOX等 | HSP相关基因 |
| 生物学意义 | T细胞功能和分化重塑 | 细胞应激适应 |
| 二者关系 | 可以同时存在 | 不是Tex的必然下一阶段 |

Chu 2023发现T_STR状态与免疫治疗抵抗有关。

但应激相关基因表达升高，本身不足以证明这些基因直接导致治疗抵抗。

---

## 6. Treg与肿瘤免疫抑制

### 6.1 Treg的正常功能

Treg（Regulatory T cell，调节性T细胞）的重要作用是维持immune tolerance（免疫耐受），避免过度免疫反应和自身免疫损伤。

但在肿瘤微环境中，部分Treg可能抑制有效的抗肿瘤免疫。

主要机制：

1. 通过CTLA-4相关机制降低抗原呈递细胞的共刺激能力。
2. 通过高表达CD25竞争局部IL-2。
3. 分泌IL-10、TGF-β等免疫调节性细胞因子。
4. 通过细胞接触及代谢调控等机制抑制其他免疫细胞。

### 6.2 FOXP3⁺CCR8⁺ Treg

- **FOXP3（Forkhead box P3，叉头框蛋白P3）**：Treg谱系及功能的重要转录因子。
- **CCR8（C-C motif chemokine receptor 8，C-C基序趋化因子受体8）**：趋化因子受体，在部分肿瘤浸润Treg中富集。

FOXP3⁺CCR8⁺表示这两个分子均呈阳性的细胞群体。

CCR8与部分肿瘤相关Treg的迁移、定位及功能状态有关。

需要注意：

- CCR8阳性不等于该细胞的抑制功能已经得到直接验证。
- FOXP3或CTLA4等基因在不同T细胞状态中可能出现表达重叠。
- 共享基因表达特征不能证明细胞具有相同的谱系身份。

---

## 7. TME、TIME与T细胞克隆扩增

### 7.1 肿瘤微环境

**TME（Tumor microenvironment，肿瘤微环境）**包括：

- 肿瘤细胞
- 免疫细胞
- 基质细胞及血管
- 细胞外基质
- 细胞因子和代谢物等

**TIME（Tumor immune microenvironment，肿瘤免疫微环境）**主要强调肿瘤中的免疫细胞组成、功能状态和相互作用。

常见免疫细胞：

| 细胞 | 主要功能 |
|---|---|
| CD8⁺ T cells | 细胞毒性杀伤 |
| CD4⁺ T cells | 协调和调节免疫反应 |
| Treg | 免疫调节与抑制 |
| NK cells（自然杀伤细胞） | 先天性细胞毒性杀伤 |
| B cells（B细胞） | 抗体反应、抗原呈递等 |
| DCs（树突状细胞） | 抗原呈递及初始T细胞激活 |
| Macrophages（巨噬细胞） | 吞噬、炎症调节、抗原呈递及免疫抑制等 |

不同免疫细胞共同构成肿瘤局部免疫生态，影响抗肿瘤免疫及治疗结局。

### 7.2 TCR克隆性

TCR通过V(D)J recombination（V(D)J基因重排）产生高度多样性。

**TCR clonotype（TCR克隆型）**：根据TCR序列定义的克隆身份。

**Clonal expansion（克隆扩增）**：具有特定TCR的T细胞克隆在刺激后发生增殖。

```text
具有特定TCR的T细胞
          ↓
       抗原刺激
          ↓
       克隆增殖
          ↓
多个具有相同TCR克隆型的细胞
          ↓
可能分布于不同转录状态或组织
```

TCR数据能够帮助分析：

- 哪些T细胞克隆发生扩增。
- 不同细胞状态是否具有克隆关联。
- 不同组织或时间点之间是否共享T细胞克隆。

注意区分：

- **Clonal expansion（克隆扩增）**：支持某个T细胞克隆发生增殖。
- **Clonal sharing（克隆共享）**：支持不同细胞群之间存在克隆关联。
- **Tumor reactivity（肿瘤反应性）**：T细胞能够识别肿瘤相关抗原。

克隆扩增不等于已证明肿瘤反应性；共享TCR也不能直接证明细胞的分化方向。

---

## 8. ICB免疫治疗与治疗抵抗

### 8.1 免疫检查点

Immune checkpoints（免疫检查点）能够限制过度T细胞活化，维持免疫稳态。

常见抑制性受体：

| 受体 | 全称及中文 | 主要作用 |
|---|---|---|
| PD-1 | Programmed cell death protein 1（程序性细胞死亡蛋白1） | 抑制部分T细胞活化相关信号 |
| CTLA-4 | Cytotoxic T-lymphocyte-associated protein 4（细胞毒性T淋巴细胞相关蛋白4） | 负向调节共刺激 |
| TIM-3 | T-cell immunoglobulin and mucin-domain containing-3（T细胞免疫球蛋白及黏蛋白结构域蛋白3） | 与部分激活和耗竭状态相关 |
| LAG-3 | Lymphocyte activation gene 3（淋巴细胞活化基因3） | 参与免疫调节 |

PD-1由PDCD1基因编码；CTLA-4由CTLA4基因编码。

### 8.2 ICB作用机制

ICB（Immune checkpoint blockade，免疫检查点阻断）通过阻断特定免疫抑制性信号，增强或恢复部分抗肿瘤免疫反应。

常见治疗：

- Anti-PD-1
- Anti-PD-L1
- Anti-CTLA-4
- Anti-PD-1 + Anti-CTLA-4

ICB不意味着所有Tex都能够完全恢复正常功能。

部分具有前体耗竭特征的T细胞可能是治疗后增殖反应的重要来源。

### 8.3 免疫治疗抵抗

免疫治疗不应答可能涉及：

- 肿瘤抗原缺乏或抗原呈递缺陷。
- 缺乏有效的肿瘤反应性T细胞。
- T细胞处于难以恢复的功能或分化状态。
- Treg等免疫抑制性细胞的作用。
- 肿瘤微环境中的代谢和应激压力。
- 肿瘤细胞自身的免疫逃逸机制。

因此，免疫治疗应答通常不能仅由单个marker gene或某一种T细胞亚群解释。

---

## 9. 临床应答与预后

### 9.1 常见临床指标

| 指标 | 全称及中文 | 含义 |
|---|---|---|
| R / NR | Responder / Non-responder（应答者/非应答者） | 根据研究规定的标准进行分组 |
| CR | Complete response（完全缓解） | 达到病灶完全缓解的规定标准 |
| PR | Partial response（部分缓解） | 肿瘤负荷达到规定程度的下降 |
| SD | Stable disease（疾病稳定） | 未达到PR或PD标准 |
| PD | Progressive disease（疾病进展） | 达到疾病进展判定标准 |
| MPR | Major pathological response（主要病理缓解） | 新辅助治疗后残余存活肿瘤通常≤10% |
| RFS | Recurrence-free survival（无复发生存期） | 从规定起点到复发或死亡的时间，具体定义依研究而定 |

### 9.2 治疗应答与预后的区别

- **Treatment response（治疗应答）**：评价肿瘤对治疗的反应。
- **Prognosis（预后）**：评价患者后续的疾病结局。
- **MPR**：侧重病理学治疗反应。
- **RFS**：侧重后续复发风险及生存结局。

患者没有达到MPR，不意味着必然很快复发。

不同T细胞状态和TIME组成可能进一步与患者复发风险相关。

---

## 10. 单细胞结果的生物学解释

### 10.1 常见概念

- **Marker gene（标记基因）**：辅助识别特定细胞群或状态的基因。
- **Gene signature（基因特征集）**：共同表征某种细胞状态或生物学程序的一组基因。
- **Transcription factor, TF（转录因子）**：能够参与调控基因转录的蛋白质。
- **Regulon（调控子网络）**：转录因子及其潜在靶基因构成的调控关系。
- **Pseudotime（伪时间）**：根据细胞分子特征推断的潜在状态变化顺序。

### 10.2 不同证据的解释边界

| 分析结果 | 可以支持 | 不能直接证明 |
|---|---|---|
| Marker genes | 细胞注释和状态识别 | 某基因必然驱动该状态 |
| Gene signatures | 某种转录程序富集 | 该程序对应功能一定实际发生 |
| Regulons | 潜在转录调控关系 | 所有调控关系都真实存在 |
| TCR clonotypes | 细胞之间的克隆关联 | 细胞分化方向 |
| Pseudotime | 潜在状态变化顺序 | 真实时间和直接谱系关系 |
| Clinical association | 细胞状态与临床结局存在关联 | 细胞状态直接导致临床结局 |

对于图谱类研究，需要始终区分：

**观察到的表达特征、推断的生物学关系，以及经过实验验证的功能机制。**

---