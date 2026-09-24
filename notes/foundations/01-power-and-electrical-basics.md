# Data Center Power & Electrical Basics

**阅读定位：** 建立从电网到芯片的供电链路，区分变压器、开关设备、UPS、配电和机柜电源的功能。

**阅读提示：** 先区分设备的功能与安装位置，再讨论技术变化是否会取消某个产品。

[返回学习目录](../../README.md) · [查看原Word笔记](../../originals/01_Data_Center_Power_and_Electrical_Infra_Basics.docx)

**对应原文：** [原文HTML归档](../../references/semianalysis-datacenter-anatomy-1-electrical.html) · [原文网站](https://newsletter.semianalysis.com/p/datacenter-anatomy-part-1-electrical)

---

**How power moves from the grid to the chip**

| **Grid / on-site generation → voltage transformation → switching & protection → backup / ride-through → low-voltage distribution → rack power conversion → chip-level voltage regulation.**<br><br>**Main Source from Semi：**[**Datacenter Anatomy Part 1: Electrical Systems**](https://newsletter.semianalysis.com/p/datacenter-anatomy-part-1-electrical) |
| --- |

## Core takeaways

- **Keep voltage high for as long as practical.** For a given power level, higher voltage means lower current, which reduces I²R losses and conductor size. Voltage is stepped down only as power gets closer to the load.

- **A data center is built around both capacity and continuity.** The electrical system must deliver enough MW while also surviving equipment failure, maintenance and utility outages.

- **Main power chain layers.** Utility / substation → MV distribution → transformers → LV switchgear → UPS / backup → PDU or busway → rack → PSU / power shelf → VRM → CPU / GPU.

- **Transformers change voltage; switchgear routes and protects power.** Transformers step AC voltage up or down; switchgear isolates, distributes, protects and meters circuits.

- **UPS and generators solve different time horizons.** UPS batteries respond almost instantly and bridge short interruptions; generators cover longer outages after they start and stabilise.

- **Redundancy is a design choice, not a single standard architecture.** N, N+1, 2N, distributed redundancy designs trade off resilience, utilisation and capex.

- **Facility power** **vs IT power.** Utility / facility capacity includes IT plus cooling and other loads（PUE）; Critical IT Power refers only to servers, storage and networking.

- **AC dominates traditional facility distribution, while chips ultimately run on DC.** Conventional data centers distribute AC through much of the facility, then convert it to DC in server PSUs or rack power shelves before final chip-level regulation.

<br>

## 1. The power path: grid to rack

| **Stage** | **Typical voltage / form** | **Main equipment** | **What it does** |
| --- | --- | --- | --- |
| **1. Utility / transmission** | HV or MV AC | Grid, transmission line, utility feed | Brings bulk power to the campus. |
| **2. Site substation** | HV → MV AC | HV transformer, HV/MV switchgear | Steps transmission voltage down and distributes power across the campus. |
| **3.** **Building distribution** | MV → LV AC | MV switchgear, MV/LV transformer | Brings voltage down to a level usable by facility electrical systems. |
| **4. Backup & transfer** | Typically LV AC in traditional designs | Generator, ATS, UPS, batteries | Maintains power through grid outages and short interruptions. |
| **5. Data-hall distribution** | LV AC | LV switchgear, PDU, RPP, busway, tap-off, power whips | Splits, protects, meters and routes power to rows and racks. |
| **6. Rack conversion** | AC → DC | Rack PDU, PSU or central power shelf | Converts facility AC into DC suitable for IT hardware. |
| **7. Board / chip** | DC → lower DC rails | DC/DC converters, VRMs | Steps voltage down to the very low voltages required by CPUs, GPUs and memory. |

### Why power is stepped down gradually

- Power loss in a conductor is approximately P_loss = I²R. For the same delivered power, raising voltage reduces current and therefore reduces resistive loss.

- High and medium voltage are efficient for bulk transport, but require more insulation, clearance and safety controls. Lower voltage is therefore used closer to people and IT equipment.

- In traditional architectures, a hyperscale campus may receive transmission-level power, step it to ~11–35 kV MV, and then step again to ~400–480 V class LV before the data hall. Exact values vary by country and operator.

### Facility power vs. Critical IT power

| **Metric** | **Meaning** |
| --- | --- |
| **Utility / Facility Power** | Total electrical capacity available to the site, covering IT plus cooling, lighting and other facility loads. |
| **Critical IT Power** | Power capacity allocated to IT equipment only: servers, storage and networking. |

<br>

## 2. What each major component actually does

| **Term** | **Plain-English function** |
| --- | --- |
| **Transformer** | Changes AC voltage level through electromagnetic induction. It does not 'distribute' loads; its core job is **voltage transformation**. |
| **Switchgear** | A protected assembly containing breakers, switches, metering and relays. It routes, isolates and protects electrical circuits. |
| **Circuit breaker** | Interrupts abnormal current to protect equipment and prevent damage or fire. |
| **ATS — Automatic Transfer Switch** | Mechanically transfers a load between normal and backup sources, commonly utility and generator. |
| **STS — Static Transfer Switch** | Uses power electronics to transfer between two AC sources much faster than an ATS, typically downstream in critical distribution. |
| **UPS — Uninterruptible Power Supply** | Provides near-instant ride-through and power conditioning. Traditional double-conversion UPS uses rectifier + battery + inverter. |
| **Generator** | Provides longer-duration backup power after startup. In traditional hyperscale designs, large diesel or gas generators are common. |
| **PDU — Power Distribution Unit** | A broad term. Facility / floor PDUs distribute power downstream; rack PDUs distribute power within the rack. |
| **RPP — Remote Power Panel** | A smaller downstream panel that splits a larger feed into multiple protected branch circuits feeding racks. |
| **Busway / busbar** | A rigid high-current distribution conductor, often with tap-off points. Common in high-density data halls because it is modular and compact. |
| **Power whip** | A flexible cable assembly that carries power from a PDU / RPP / busway tap-off to the rack. |
| **PSU — Power Supply Unit** | Converts incoming AC to DC for server electronics in conventional server designs. |
| **Power shelf** | Centralises AC-to-DC conversion for an entire rack and feeds servers through a DC busbar; common in OCP-style architectures. |
| **BBU — Battery Backup Unit** | A distributed battery module close to the rack / load, providing short-duration backup without relying on a central UPS. |
| **VRM — Voltage Regulator Module** | Final-stage DC/DC conversion on or near the compute board, stepping the bus voltage down to chip-level rails. |

<br>

## 3. Redundancy: how data centers avoid a single point of failure

### The basic language

| **Architecture** | **Simple interpretation** |
| --- | --- |
| **N** | Exactly the capacity required for normal operation; no spare capacity. |
| **N+1** | Required capacity plus one additional component. If one unit fails or is maintained, the spare can cover it. |
| **N+X** | Required capacity plus X additional units. |
| **2N** | Two complete, independent systems, each capable of supporting the full load. |
| **2N+1** | Two full systems plus an additional spare element. |
| **Distributed redundant / catcher** | Shared spare capacity is distributed across multiple blocks so utilisation is higher than a simple 2N design. |
| **3N/2** | Infrastructure sized to 1.5× the base load, providing redundancy with less duplication than 2N. |

### How redundancy is implemented in practice

- Traditional colocation designs often use independent A-side and B-side power paths. Dual-corded IT equipment can continue operating if one path is lost.

- A Tier III / Rated 3 style design is commonly described as concurrently maintainable: planned maintenance can be performed without taking the IT service offline.

- Tier IV / Rated 4 adds fault tolerance: a single unexpected infrastructure failure should not interrupt the critical load.

- Hyperscalers may use architectures such as distributed redundancy, catcher systems or 4N3R rather than simple 2N, because these can improve asset utilisation and reduce capex per MW.

### UPS vs. generator: the timing stack

| **Layer** | **Response / duration** | **Role** |
| --- | --- | --- |
| **UPS / BBU** | Milliseconds to minutes | Instant ride-through; keeps IT alive while another source starts or transfers. |
| **Generator** | Tens of seconds onward | Longer-duration backup after startup and stabilisation. |
| **Grid / utility** | Normal operating source | Primary energy supply in a conventional data center. |

<br>

## 4. AC vs. DC: the minimum you need to know

### Why traditional data centers are mostly AC-distributed

- The public grid is AC, and AC voltage can be stepped up or down efficiently with mature transformer technology.

- Facility loads such as chillers, pumps, fans, lighting and many building systems are conventionally designed around AC.

- Traditional server architectures therefore bring AC close to the rack and convert it to DC inside server PSUs or rack-level power shelves.

### Why IT electronics ultimately need DC

- Semiconductor devices do not operate directly from facility AC. CPUs, GPUs, memory and storage electronics require regulated DC rails.

- The power chain therefore contains one or more AC/DC and DC/DC conversion stages before power reaches the silicon.

- OCP-style racks centralise AC/DC conversion in a power shelf and distribute DC within the rack, instead of putting a separate rectifier inside every server.

### Single-phase vs. three-phase AC

|  | **Single-phase** | **Three-phase** |
| --- | --- | --- |
| **Typical use** | Lower-power equipment and small loads | Data-center distribution and high-power equipment |
| **Why it matters** | Simple but lower power density | Higher power delivery for a given conductor / installation |

### Typical voltage examples — directional, not universal

- North America: 120/208 V is common for smaller loads; 480 V three-phase is common in higher-power facility distribution.

- Europe: ~230 V single-phase and ~400 V three-phase are common.

- Asia-Pacific: standards vary by country; ~220–230 V single-phase and ~380–400 V three-phase are common in many markets.

## 5. Essential terms

| **Term** | **Meaning** |
| --- | --- |
| **HV / MV / LV** | High / Medium / Low Voltage. Exact boundaries depend on standards and jurisdiction. |
| **MVA vs. MW** | MVA is apparent AC power; MW is real power. The ratio is governed by power factor. |
| **Power factor** | Ratio of real power to apparent power in an AC system. |
| **Critical IT Power** | Capacity reserved for servers, storage and networking. |
| **Data hall** | Room containing IT racks. |
| **Pod** | A modular block of IT capacity with a dedicated or semi-dedicated set of electrical / cooling infrastructure. |
| **White space** | Area occupied by IT racks and rack-adjacent equipment. |
| **Grey space** | Electrical / mechanical support area outside the main IT white space. |

A-side / B-side = two independent power paths for distribution redundancy; PUE = total facility energy ÷ IT equipment energy.

---

[下一篇：散热系统基础](../foundations/02-cooling-system-basics.md)
