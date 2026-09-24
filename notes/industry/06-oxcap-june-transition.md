# 800V DC Datacenter Transition

**阅读定位：** 在迁移框架上加入多种架构并存、DC保护需求及既有供应商适应能力。

**阅读提示：** 来源日期为2026年6月2日；应与九月CMD报告分开阅读，厂商判断保留当时归属。

[返回学习目录](../../README.md) · [通篇逻辑梳理](../../STUDY_MAP.md) · [查看原Word笔记](../../originals/06_Oxcap_800VDC_Notes.docx)

**对应原文：** [原文PDF](../../references/oxcap-800vdc-transition-2026-06-02.pdf) · [出版方网站](https://oxcapanalytics.com/)

---

**Reading Notes**

Based on Oxcap Analytics, 2 June 2026

| **THE CORE MESSAGE**<br>**The investment implication is a reallocation of value, not a simple collapse in electrical content.**<br>Higher rack density pushes the IT power train toward higher-voltage DC, but the transition will be gradual and heterogeneous. Traditional LV AC categories face pressure, while DC power electronics, storage, protection and control expand. The main uncertainty is therefore who captures the new value pools—and how quickly incumbents can pivot.<br><br>**This is a report based** **on** **Semi Analysis** **“Inside the 800VDC Revolution** **–** **Part 1”.** |
| --- |

## Core takeaways

- **Physics, not preference.** At very high rack densities, low-voltage architectures drive excessive current, copper, losses and space. Higher-voltage DC therefore becomes increasingly necessary.

- **The value pool shifts more than it shrinks.** Oxcap cites a SemiAnalysis framework in which electrical supplier TAM moves only modestly from c.$3.35m/MW today to c.$3.05m/MW in Phase 4, but the **product mix changes materially**.

- **Phase 1 is broadly additive.** The near-term sidecar architecture removes the rack PDU but adds an HVDC power rack, conversion, storage and controls. Oxcap therefore expects the technology impact on vendor growth to become more visible only around 2028–29.

- **The transition will be fluid, not a single four-step industry standard.** NVIDIA-led designs may move faster, while ASIC, AMD and Chinese architectures may follow different paths. Conventional AC will remain relevant for lower-density IT and non-IT facility loads.

- **Supplier outcomes are not binary.** Product exposure matters, but scale manufacturing, qualification, customer relationships, partnerships, M&A and the ability to redesign portfolios can be just as important.

- **DC creates new protection requirements.** Because DC has no natural current zero-crossing, protection, isolation, monitoring and fault management become more demanding—an incremental opportunity that Oxcap believes may be underappreciated.

<br>

## 1. How Oxcap frames the transition

### A three-layer lens

| **Lens** | **What it means** |
| --- | --- |
| **Power consumption vs. unit volume** | Products that scale with MW (generation, MV equipment, secure power, cooling) benefit more directly from rising power density than products tied to rack count (cabinets, cable management, some PDUs). |
| **Equipment lifespan** | Long-life grid and transformer assets can last decades; equipment closer to the server may be redesigned every compute cycle. As AI capex normalises, replacement-cycle exposure becomes more important. |
| **Technology transition** | 800V DC, liquid cooling and higher rack density can reallocate value pools, invite new entrants and increase R&D / qualification costs. The shift from electromechanical equipment toward electronics may also change margin structures. |

### Oxcap’s key differentiation vs. SemiAnalysis

- **Transition path:** Oxcap expects multiple architectures to coexist rather than a rigid four-phase migration.

- **Broader technology set:** NVIDIA is important, but Google/Amazon ASICs, AMD and Chinese accelerators may drive different electrical designs.

- **Underappreciated DC content**: DC still requires switching, protection, sensing, monitoring, arc-fault detection and battery management; these can offset part of the loss in traditional AC equipment.

- **Incumbent advantage**: technology alone does not determine winners. Customers (Hyperscaler) value supply scale, quality, delivery reliability and a diversified vendor base. Incumbents can adapt through R&D, partnerships, licensing and M&A; Oxcap therefore rejects a simple ‘winner / loser’ framing.

## 2. The four-phase roadmap — simplified

| **Phase** | **Architecture change** | **Main value shift** | **Oxcap read** |
| --- | --- | --- | --- |
| **1 \| ~2027+** | HVDC sidecar replaces rack PDU at the row / rack interface. | Adds rectification, BBU / buffering, controls and protection. | Broadly additive; sidecar is a large but potentially temporary opportunity. |
| **2 \| ~2028+** | Rack becomes 800V DC native; DC/DC conversion moves closer to the compute blade. | LV UPS role declines; spend shifts to BBUs, PSUs and rack-level power electronics. | More structural shift; adoption still customer-specific. |
| **3 \| ~2028/29+** | AC/DC rectification moves upstream; 800V DC becomes the distribution backbone. | Less LV AC gear; more DC busway, battery racks, DC protection and controls. | Value is redistributed rather than simply eliminated. |
| **4 \| >2029** | MV AC converts directly to 800V DC via solid-state transformers. | Traditional LV AC chain largely disappears; SST becomes a new major category. | Most disruptive, but also the least mature and least certain. |

<br>

## 3. What changes by phase

### Phase 1 — Sidecar: a transitional, additive architecture

- Most upstream infrastructure remains AC: MV equipment, transformers, UPS and 415V AC distribution stay in place.

- A rack-adjacent HVDC sidecar converts 415V AC to 800V DC and can integrate BBU / supercapacitor buffering for GPU load swings.

- The traditional rack PDU is reduced or removed, but new conversion, protection and control content more than offsets it in the near term.

- SemiAnalysis estimates the sidecar opportunity could peak at about $11bn in 2028; Oxcap sees Schneider, Vertiv, Eaton, Delta and ABB as likely participants.

### Phase 2 — DC-native rack

- 800V DC penetrates deeper into the rack; DC/DC conversion moves closer to the compute blade.

- Central LV UPS can lose relevance as batteries and protection migrate toward the rack; some operators may retain LV UPS or move backup upstream to MV UPS.

- Value shifts toward BBUs, PSUs, power modules and other electronics—areas where Delta, Lite-On, Flex Power and similar suppliers are stronger.

### Phase 3 — Centralised 800V DC distribution

- Rectification moves into grey space / outdoors, creating an 800V DC backbone feeding rows and racks.

- MV transformers and switchgear remain; much of the LV AC chain is simplified or removed.

- DC busway, battery racks, DC switchgear / breakers, solid-state protection and monitoring become new or larger spend pools.

### Phase 4 — Solid-state transformer architecture

- SSTs convert MV AC directly to low-voltage DC using high-frequency semiconductor switching, potentially removing multiple conversion stages.

- Strategic benefits: smaller footprint, higher controllability and potentially bidirectional grid interaction.

- Key constraint: maturity and mission-critical reliability. Broad adoption is not expected before 2029.

- Oxcap highlights a new competitive field spanning start-ups, transformer incumbents and semiconductor suppliers; this is not automatically captured by today’s LV electrical leaders.

## 4. Facility-level implications

- The data centre does not become fully DC. Chillers, pumps, fans, lighting, HVAC and building controls remain largely AC, so hybrid AC/DC facilities are the likely outcome.

- Long-duration backup does not disappear. BBUs, batteries and supercapacitors handle transients and ride-through, while generators, fuel cells or other long-duration sources remain relevant.

- Safety and approval are gating factors. DC arcs are harder to interrupt than AC, requiring DC-rated breakers, isolation, fault detection and potentially solid-state protection. Oxcap expects standards and local approvals to remain an adoption constraint.

<br>

## 5. Supplier implications — Oxcap’s view

| **Vendor** | **Oxcap framing** | **Why** |
| --- | --- | --- |
| **Delta Electronics** | Best positioned | Strong power-electronics / DC capability; broad white-space exposure; less legacy AC disruption. |
| **Vertiv** | Relatively well positioned | Lower exposure to categories most at risk; strong cooling and electronics content. UPS could become a later headwind. |
| **ABB** | Balanced / potentially stronger than perceived | MV exposure is resilient; strong DC heritage and protection capability. Some LV AC content still needs to migrate. |
| **Siemens** | Balanced | High MV exposure and no UPS exposure are positives; LV electrical exposure may be underappreciated. |
| **Schneider Electric** | Mixed but adaptable | UPS / secure power exposure creates risk, but scale, MV strength, sidecar/DC products and system-integration capability provide offsets. |
| **Eaton** | Mixed but improving | UPS exposure is at risk, but battery, DC architecture and the Resilient Power Systems SST acquisition broaden the opportunity. |
| **Legrand** | Most exposed near term | Rack PDU / row-level exposure is pressured in Phase 1; DC busway, cooling, M&A and portfolio adaptation provide potential offsets. |

---

[上一篇：SemiAnalysis迁移框架](../industry/05-semianalysis-transition.md) · [下一篇：Oxcap九月：增长与利润率](../industry/07-oxcap-september-cmd.md)
