# NVIDIA 800 VDC Architecture - Version 1

**阅读定位：** 从计算平台设计者视角理解800VDC、负载波动、分层储能和电压选择。

**阅读提示：** 这是第一版白皮书的既有笔记。原笔记中标为个人补充的内容，以及有条件的效率、导体利用率比较，应与NVIDIA原文观点区分。

[返回学习目录](../../README.md) · [查看原Word笔记](../../originals/04_NVIDIA_800VDC_Architecture_Key_Notes.docx)

---

Whitepaper Reading Notes - Key Takeaways

## Key Concepts

- **Rack power, not chip TDP alone, is the driver.** GPU TDP typically rises incrementally, but larger NVLink domains can push rack power up by multiples. Hopper to GB300 is NVIDIA's example: +75% TDP, ~50x performance and ~3.4x rack power density.

- **800 VDC solves both scale and space constraints.** Higher voltage reduces current for the same power, cutting conductor size, cable bulk and rack/facility power-distribution footprint. NVIDIA cites +157% power transfer through the same copper cross-section versus 415 VAC.

- **Energy storage becomes part of the power architecture, not an optional add-on.** Synchronized GPU workloads can swing between ~30% and 100% rack power. Storage is used to smooth these swings before they propagate to the data center and grid.

- **Storage must be layered by timescale.** Electrolytic capacitors are best suited to sub-100 ms events; mixed technologies cover ~100 ms to 10 s; batteries become more volume-efficient at longer durations.

- **The migration path is staged.** Near term: side power racks for brownfield retrofits. Next: facility-level LV AC-to-800 VDC rectification. Longer term: MV rectifiers or solid-state transformers (SSTs) converting MV AC directly to 800 VDC.

- **800 VDC is the practical near-term choice; 1500 VDC is a longer-term option.** 1500 VDC improves conductor utilization further, but indoor IT safety standards, certified components, creepage/clearance and arc-flash constraints are less mature.

**Source:** [NVIDIA 800 VDC Architecture - official page / whitepaper access](https://www.nvidia.com/en-us/data-center/technologies/800-vdc-architecture/)

<br>

## 1. Why the power architecture has to change

- GPU generations increase chip power, but the bigger step-change comes from putting more GPUs into one tightly coupled NVLink domain. NVIDIA notes that rack power can rise 2x / 4x / 8x as the networking domain expands.

- **Copper is preferred for short-reach GPU interconnect because of performance and cost**, so maximum compute performance increasingly depends on packing more GPUs into a limited physical radius - directly linking performance to power density.

- Power infrastructure is therefore moving from a supporting function to **a primary constraint** on AI Factory design. A second design objective is to move power components out of the highest-value NVLink compute space.

## 2. Load swings make energy storage mandatory  |  The grid wants stable load; GPUs want highly dynamic power

- LLM workloads alternate between intensive matrix computation and data exchange. Without buffering, rack demand can swing from ~30% idle to 100% utilization in short time interval.

- NVIDIA describes four complementary mitigation methods: (1) reduce idle periods in software, (2) use energy storage, (3) burn power as a backstop, and (4) throttle GPU performance as a last resort.

- Best practice is to absorb most swings with storage close to the GPU, minimizing data-center slew rates and RMS-current losses; burn power and throttling remain corner-case backstops.

- Three relevant timescales: up to ~100 ms for GPU overshoot / idle events; ~1-5 s for checkpointing; minutes for full workload ramp-up / ramp-down. Storage technology should be selected accordingly.

## 3. Why 800 VDC  |  Higher voltage moves more power through less copper and with fewer conversion stages

| Voltage | Conductors | Power / cable area | vs. 415 VAC |
| --- | --- | --- | --- |
| 415 VAC | 4 | 0.6 kW/mm² | - |
| 480 VAC | 4 | 0.8 kW/mm² | +16% |
| **800 VDC** | **3** | **1.7 kW/mm²** | **+157%** |
| 1500 VDC | 3 | 3.1 kW/mm² | +382% |

- Compared with 54 VDC in-rack distribution and 480 VAC facility distribution, 800 VDC reduces current, copper usage and cable bulk.

- At the rack level, NVIDIA takes 800 VDC directly to the compute node, then converts 800 VDC to 12 VDC close to the GPU using a 64:1 LLC converter and matrix transformer.

- Safety is built around touch-safe connectors, mechanical interlocks preventing disconnect under load, reinforced isolation and DC-specific protection - drawing on mature EV practices.

## 4. Facility architecture evolution  |  From retrofit to native DC

- Today: MV step-down transformer -> LV switchboard -> AC UPS -> PDU / RPP or busway -> rack PSU -> 54 VDC.

- Near-term retrofit: add an 800 VDC side power rack next to compute racks. This is not the end-state optimum because it adds conversion stages (Less efficient), but it enables higher rack density with minimal brownfield changes.

- Longer term: MV rectifiers or SSTs convert medium-voltage AC (e.g., 35 kV) directly to 800 VDC, removing the conventional 480 VAC layer. NVIDIA views MV rectifiers as the more mature near-term path; multi-MW SSTs still face reliability and thermal/electrical-density challenges.

<br>

## 5. Grid interconnection and storage placement  |  AI Factories must become controllable electrical loads

- Large synchronized GPU clusters can create **rapid voltage and frequency deviations**. Utilities therefore increasingly require load flexibility, controllability and predictability before approving interconnection.

- Required capabilities include fast energy storage, GPU/workload pacing, coordinated compute + storage + facility controls, ramp-rate management, transient stability, harmonics/flicker control and voltage ride-through, etc.

- Storage is deployed at both ends: facility/grid-side BESS for slower, larger-scale averaging and transfer support; short-duration capacitors near racks for fast power smoothing and slew-rate control.

- Longer term, NVIDIA frames AI Factories as potential grid-supporting assets: they can absorb excess power, deliver supplemental power during stress, and support voltage/frequency stability through coordinated controls.

- Personal Notes：Another bottleneck to keep in mind is that upgrades to existing data centers may require more transformers than expected, due to US bulk power grid equipment aging: 70% of transformers have been in service for more than 25 years. Spare capacity stands at only 20%, leaving no redundant buffer to absorb frequent and large load swings.

## 6. Voltage alternatives and industry implications  |  Why 800 VDC is the near-term convergence point

- 750 VDC: mature European industrial approach with a simplified two-wire system and compatibility with many 1000 V-class components.

- +/-400 VDC: technically feasible and supported by OCP heritage, but midpoint grounding, protection and balancing become more complex at data-center scale.

- 1500 VDC: attractive for long-term conductor efficiency, but data-center indoor safety standards, certified components, clearance/creepage requirements and arc-flash controls are not yet as mature.

- 800 VDC therefore balances efficiency, equipment availability ( Adopted by EV industry ), protection simplicity and regulatory practicality, while preserving a pathway to higher voltages later.

## 7. What needs to mature in the ecosystem  |  The shift creates a new DC-native component stack

- **Standardization:** common voltage windows, connector interfaces and current ratings.

- **DC-native equipment:** rectifiers, distribution boards, breakers/protection, cabling, connectors, transfer-trip schemes and metering.

- **Safety and operations**: grounding, fault isolation, arc-flash mitigation, maintenance procedures and technician training.

---

[上一篇：为什么转向800VDC](../800vdc/03-why-800vdc.md) · [下一篇：SemiAnalysis迁移框架](../industry/05-semianalysis-transition.md)
