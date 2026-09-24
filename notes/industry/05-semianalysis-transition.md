# Inside the 800VDC Revolution - Part 1

**阅读定位：** 用四阶段框架分析设备如何增加、移位、集成与替代，以及每MW价值量的变化。

**阅读提示：** 来源日期为2026年5月26日。阶段时间、市场规模与成本均为当时的报告预测或模型假设。

[返回学习目录](../../README.md) · [查看原Word笔记](../../originals/05_SemiAnalysis_800VDC_Transition_Notes.docx)

---

**Key Reading Notes**

Based on SemiAnalysis, 26 May 2026

| **WHAT TO REMEMBER**<br>**Semi** **Analysis sees 800V DC as a staged redesign of the entire AI data** **center** **power chain, not a single voltage change.** The near-term opportunity is the HVDC sidecar; the structural change comes when 800V DC becomes facility-wide; the long-term prize is the SST. Across all phases, the more important question is where conversion, storage, protection and distribution functions move - and which suppliers capture those relocated value pools.<br><br>Source: [Inside the 800VDC Revolution – Part 1](https://newsletter.semianalysis.com/p/inside-the-800vdc-revolution-part) |
| --- |

## Core takeaways

- **The transition is driven by rack density and system economics.** At ~600 kW-class racks, 48-54 V distribution becomes impractical because current, copper mass, heat and power-hardware volume rise sharply. SemiAnalysis **estimates ~5%** facility-level power savings for the mature 800V DC architecture.

- **800V DC does not** **arrive** **all at once.** Phases 1-2 retrofit existing AC facilities using an **HVDC power rack / sidecar**; Phase 3 moves **rectification upstream** and makes 800V DC the hall-level backbone; Phase 4 introduces **MV** **SSTs**.

- **Phase 1 adds equipment rather than removing it.** The existing AC backbone largely remains, while a new HVDC power rack is added beside compute rack. Semi Analysis estimates: sidecar TAM peaking around $11bn in 2028.

- **Phase 2 is the first major structural inflection.** 800V DC reaches the compute blade and the role of centralized LV UPS begins to decline. BBUs and supercapacitors move resilience and transient buffering closer to the load.

- **Phase 3 shifts the data hall from AC distribution to DC distribution.** LV AC switchgear, floor PDUs and parts of the AC busway chain are removed or redesigned; MV rectifiers, battery racks and DC protection become more important.

- **Phase 4 is the SST end-state, but not yet mature.** SSTs combine MV step-down and rectification into one programmable power-electronics platform. SemiAnalysis expects meaningful adoption only from 2029 and sizes 2030 SST TAM at $32bn.

- **Total electrical spend per MW changes less than the equipment mix.** SemiAnalysis argues that value migrates across the chain: grey-space AC equipment loses share while white-space power electronics, storage and DC protection gain.

- **Execution constraints are material.** Safety, grounding, DC fault interruption, cooling / auxiliary AC loads, standards and grid-interconnection rules can slow adoption even if the core physics are compelling.

<br>

## 1. Why 800V DC becomes necessary for compute racks

- **Low-voltage current becomes the bottleneck.** At a fixed power level, higher voltage reduces current linearly. For 600 kW rack: 54 V structure requires : 11 kA; 800 V requires: 750 A, meaning significant deduction of copper usage.

- **Copper and thermal constraints** **scale** **non-linearly.** Resistive losses scale with I²R. In practice, operators use the lower current to shrink conductors and busbars while still improving efficiency and reducing weight, heat and routing space.

- **Power hardware starts to crowd out compute.** As rack power rises, low-voltage power shelves, busbars and cabling consume too much valuable rack volume. Moving to HVDC lets more of the rack remain dedicated to GPUs, networking and cooling.

- **Density improves compute economics.** Larger scale-up domains depend on tightly packed compute. SemiAnalysis links denser racks to lower cost per token, making the electrical architecture an enabler of the compute architecture rather than a standalone facility choice.

## 2. Four-phase transition at a glance

| **Phase** | **Timing** | **What changes** | **What remains** | **Key implication** |
| --- | --- | --- | --- | --- |
| **1** | 2026/27 | HVDC power rack converts AC to 800V DC near the rack. | Most grey-space AC infrastructure; UPS remains. | Retrofit / future-proofing; additive electrical content. |
| **2** | 2027/28 | 800V DC becomes native to compute; DC/DC conversion moves onto / near the blade. | Power rack retrofit remains because facility DC is not ready. | UPS begins to lose its role; distributed storage grows. |
| **3** | Late 2028/29 | Central rectifier creates a facility-level 800V DC backbone. | MV grid interface and LV transformer remain in the base case. | LV AC distribution is replaced by DC distribution and protection. |
| **4** | >2029 | SST converts MV AC directly to 800V DC. | Auxiliary AC bus for cooling / building loads remains. | Transformer + rectifier collapse into one power-electronic platform. |

### Adoption outlook

- SemiAnalysis forecasts ~39 GW of incremental capacity powered by 800V DC by 2030.

- Phases 1-2 are sidecar-heavy because the underlying facility remains AC-distributed.

- The mix shifts around 2029 as facility-level HVDC and SST / MV-rectifier architectures become viable.

- There is no single universal sidecar design: NVIDIA uses a monopolar 800V approach, while OCP Diablo 400 supports ±400V bipolar and 800V monopolar options.

<br>

## 3. Phase 1 - White-space retrofit

- **Architecture.** MV AC → LV transformer → UPS → 415/480 V AC busway remains unchanged. The new element is a HVDC power rack (Sidecar) that converts AC to 800V DC and feeds adjacent IT racks.

- **Power rack functions.** AC/DC rectification, short-duration BBU ride-through, optional capacitor / supercapacitor buffering, power management and DC output distribution.

- **Why the sidecar exists.** It separates power conversion from the compute rack, improving serviceability and preserving rack volume for compute.

- **Economics.** SemiAnalysis estimates ~$400-500k per power rack, around ~$0.5m/MW, with sidecar TAM peaking at ~$11bn in 2028.

- **Key nuance.** Phase 1 is not yet **forced** by hardware: Vera Rubin racks can still be supported by conventional three-phase AC. Early adoption is therefore mainly future-proofing and efficiency-driven.

## 4. Phase 2 - 800V DC-native compute

- **Main change.** 800V DC is routed deeper into the compute rack. Instead of a central rack-level power shelf converting 800V to ~50V, an on-blade / near-blade module performs the step-down closer to the load, which means HVDC power rack is required for the newer generation compute racks.

- **Why it matters.** This is the point where 800V DC becomes driven by rack density rather than simply by operator preference.

- **UPS transition.** Semi Analysis expects centralized LV UPS to progressively lose importance as BBU and supercapacitor storage become DC-coupled near the rack (can perform similar functionality of UPS with adoption of BESS). Google and Meta already use distributed backup approaches in parts of their fleets.

- **Not universal.** Colocation providers and less vertically integrated operators may retain LV UPS longer for redundancy, operational simplicity and support for mixed AC workloads. MV UPS and facility-level BESS are alternative backup architectures.

<br>

## 5. Phase 3 - Facility-level 800V DC distribution

- **Rectification moves upstream.** A central rectifier in grey space / outdoors converts 415V AC to 800V DC, and DC becomes the hall-level distribution backbone.

- **What disappears / shrinks.** 480V AC switchgear below the rectifier, AC floor PDUs and much of the traditional AC distribution layer are removed or redesigned.

- **What replaces it.** DC busway, DC distribution, battery racks, DC breakers / SSCBs, monitoring, etc.

- **Battery rack.** Once AC/DC conversion moves upstream, the former power rack becomes primarily an energy-storage / distribution rack: DC/DC distribution units, BBU shelves and optional supercapacitors. SemiAnalysis estimates roughly ~$200k/MW of battery-rack content.

### DC distribution and protection

- Early deployments may favour feeder-only DC busway because live tap-offs are harder to implement safely at 800V DC.

- DC has no natural zero-crossing, so fault arcs are harder to interrupt than in AC systems. This increases the importance of DC-rated breakers, isolation and solid-state circuit breakers (SSCBs).

- SemiAnalysis sees several possible distribution products: rectifiers with integrated protected outputs, breaker-equipped DC tap-offs, and prefabricated grey-space pods combining rectifier + distribution + busway.

## 6. Phase 4 - SST end-state

- **Architecture.** The SST replaces the LV transformer + LV AC/DC rectifier with a single MV-AC-to-800V-DC power-electronic system.

- **Why SSTs are attractive.** Higher switching frequency enables a much smaller transformer core; SSTs also support active regulation, software control and potentially bidirectional power flow.

- **Technology stack.** MV input stages rely on high-voltage SiC devices (3.3 kV-class and above); downstream 800V conversion can use lower-voltage SiC / GaN devices.

- **Current maturity.** Public prototypes are around ~98-98.5% efficiency; the datacenter target is multi-MW units approaching 99%+ continuous efficiency with proven reliability.

- **Economics.** SemiAnalysis estimates SST content at ~$1.0-1.5m/MW and 2030 SST TAM at ~$32bn, with significant competition from MV rectifiers.

- **Timing.** Broad adoption is not expected before ~2029; certification, reliability and standards remain gating factors.

<br>

## 7. How the equipment value pool moves

| **Category** | **Direction** | **SemiAnalysis logic** |
| --- | --- | --- |
| **Central LV UPS** | Down | Ride-through and buffering migrate toward DC-coupled BBU / supercapacitor architectures; not all operators will eliminate UPS immediately. |
| **Rack PDU / traditional rack AC power** | Down | High-density racks increasingly receive HVDC rather than conventional AC at the rack interface. |
| **LV AC switchgear / floor PDU** | Down in Phase 3+ | Removed when 800V DC becomes the hall-level distribution backbone. |
| **HVDC power rack / sidecar** | Up, then down | Large Phase 1-2 opportunity, but temporary as rectification moves upstream. |
| **DC busway & protection** | Up | New DC distribution needs busway, breakers / SSCBs, isolation, sensing and monitoring. |
| **BBU / supercapacitors** | Up | Storage moves closer to compute to provide ride-through and absorb fast GPU transients. |
| **SST / MV rectifier** | Up materially | Phase 4 shifts conversion value upstream; SST becomes a new high-value category. |
| **MV switchgear / grid interface** | Largely resilient | Utility and most on-site generation remain AC; upstream MV infrastructure remains necessary. |
| **Cooling / auxiliaries** | Mostly AC | Chillers, pumps, fans, lighting and building systems still require an auxiliary AC bus, although DC-native components are emerging. |

## 8. Key implementation challenges

- **Safety and fault interruption.** 800V DC requires new procedures for arc management, isolation, de-energisation and technician training.

- **Grounding architecture.** ±400V bipolar and 800V monopolar systems create different protection-device, insulation-monitoring and fault-behaviour requirements; industry consensus is not yet established.

- **Cooling and auxiliary loads.** The IT power chain can move to DC faster than the rest of the facility. Cooling, lighting, fire systems and building controls keep an AC auxiliary bus relevant.

- **Standards and certification.** Busway standards are progressing, but many 800V DC categories still require site-specific engineering and AHJ / certification approval.

- **Grid interconnection.** SST control, BESS state of charge and highly dynamic GPU loads change the facility’s grid-facing behaviour, increasing requirements for dynamic modelling, ride-through and utility coordination.

---

[上一篇：NVIDIA第一版架构笔记](../800vdc/04-nvidia-v1-architecture.md) · [下一篇：Oxcap六月：价值迁移与供应商适应](../industry/06-oxcap-june-transition.md)
