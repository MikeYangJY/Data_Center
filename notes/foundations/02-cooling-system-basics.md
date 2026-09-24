# Data Center Cooling Systems

**阅读定位：** 建立从芯片到室外环境的散热链路，理解风冷、液冷、CDU与设施排热之间的关系。

**阅读提示：** 本文基于2025年的来源材料；功率、风量和容量数字应按案例条件理解。

[返回学习目录](../../README.md) · [查看原Word笔记](../../originals/02_Data_Center_Cooling_System_Basics%20%28Semi%29.docx)

**对应原文：** [原文HTML归档](../../references/semianalysis-datacenter-anatomy-2-cooling.html) · [原文网站](https://newsletter.semianalysis.com/p/datacenter-anatomy-part-2-cooling-systems)

---

**Notes based on** **SemiAnalysis（Cooling）, 2025**

| **Cooling architecture is moving closer to the heat source as AI rack density rises.** Traditional room-level air cooling remains highly relevant, but higher-density AI systems increasingly require rack-level or chip-level liquid cooling, supported by CDUs, facility water loops and heat-rejection equipment.<br><br>Main Source from Semi：[Datacenter Anatomy Part 2 – Cooling Systems](https://newsletter.semianalysis.com/p/datacenter-anatomy-part-2-cooling-systems) |
| --- |

## Core takeaways

- **Heat follows power.** Almost all electrical power consumed by IT equipment becomes heat. Higher chip and rack power therefore translates directly into higher cooling requirements.

- **The real problem is heat density, not simply total MW.** Air cooling can be very efficient at lower densities, but moving large amounts of heat from a small rack footprint requires rapidly increasing airflow, fan power and space.

- **Liquid cooling moves heat removal closer to the source.** RDHx removes heat at the rack exhaust; Direct-to-Chip Liquid Cooling (DLC) removes heat directly from CPUs/GPUs through cold plates.

- **Liquid cooling does not eliminate facility cooling infrastructure.** Heat still has to move from the chip or rack to a CDU / facility water loop and then to chillers, dry coolers, cooling towers or other heat-rejection systems.

- **Hybrid cooling is normal.** A rack or data hall can combine DLC with air cooling or RDHx because not every component is necessarily liquid-cooled and legacy facilities may lack full liquid infrastructure.

- **CDU is the bridge between IT liquid loops and facility water.** It typically contains a liquid-to-liquid heat exchanger, pumps and controls, managing temperature, flow and pressure while isolating the two loops.

- **Cooling efficiency is a system-level trade-off.** PUE, WUE, inlet temperature, Delta T, fan energy, pump energy, chiller load and climate all matter. Optimising one metric can worsen another.

- **Free cooling and higher operating temperatures can materially reduce energy use.** Hyperscalers achieved low PUE partly by using outside air / water conditions, higher inlet temperatures and highly optimised airflow.

Context note:  not a current market forecast or a definitive 2026 technology roadmap.

<br>

## 1. Cooling basics: how heat leaves a data center

| **Stage** | **Heat-transfer medium** | **Typical equipment** | **Function** |
| --- | --- | --- | --- |
| **1. Chip / server** | Silicon → metal → air or liquid | TIM, heat sink, cold plate, server fans | Moves heat away from the chip package. |
| **2. Rack / data hall** | Air and/or liquid | Fans, containment, RDHx, DLC loop | Collects heat from IT equipment. |
| **3. Facility loop** | Water / coolant | CRAH, fan wall, CDU, pumps, heat exchangers | Transfers heat from the IT area to central cooling infrastructure. |
| **4. Refrigeration / economiser** | Refrigerant and/or facility water | Chiller, waterside / airside economiser | Lowers coolant temperature when ambient conditions alone are insufficient. |
| **5. Heat rejection** | Air and/or evaporating water | Dry cooler, air-cooled chiller, cooling tower | Rejects heat into the outside environment. |

### Key physical concepts

- 1 kW of IT power produces approximately 1 kW of heat that must ultimately be removed.

- Delta T is the temperature difference between inlet and outlet. A larger useful Delta T can reduce the airflow or liquid flow required to remove a given amount of heat.

- Fan power is highly nonlinear: under the fan laws, power scales approximately with the cube of fan speed. Small reductions in airflow can therefore generate large energy savings.

- SemiAnalysis cites ~165-170 CFM of airflow per kW of heat as a common rule of thumb for air-cooled servers.

### PUE and WUE

| **Metric** | **Definition** | **What to remember** |
| --- | --- | --- |
| **PUE** | Total facility power / IT power | Lower is better, but comparisons can be distorted by where fan / pump power is counted. |
| **WUE** | Water use per unit of IT energy | Captures the water trade-off; evaporative systems can lower energy use but consume more water. |

<br>

## 2. Air-cooled architecture and indoor cooling units

| **Technology** | **Where it sits** | **How it works** | **Typical positioning in the report** |
| --- | --- | --- | --- |
| **CRAC** | Data hall | Local refrigeration cycle using refrigerant; paired with an outdoor condenser. | Simple but lower-capacity / lower-efficiency; more common in legacy or small facilities. |
| **CRAH** | Data hall | Fans blow return air across a coil supplied by central facility chilled water. | Better economics at scale but requires central piping, pumps and chillers / towers. |
| **Fan Wall** | Data hall / mechanical corridor | Large banks of fans and cooling coils move high volumes of air across an entire hall. | SemiAnalysis cites ~500-600 kW per unit; scalable for 5-10 MW data halls. |
| **RDHx** | Rack rear door | Water-cooled radiator captures heat from server exhaust air at the rack. | ~30-40 kW passive; >50 kW with active fans in the report. Often used as a bridge / hybrid solution. |

### Why airflow management matters

- Hot and cold air mixing wastes temperature headroom. Containment separates supply and return air and allows higher, more controlled inlet temperatures.

- Modern greenfield facilities often use hot-aisle containment; cold-aisle containment also exists, but layout and maintenance trade-offs differ.

- Hyperscalers use CFD (Computational Fluid Dynamics) to reduce recirculation, bypass airflow and unnecessary fan power.

### RDHx: why it matters

- RDHx can be thought of as an 'in-rack air handler': servers remain air-cooled, but rack exhaust heat is transferred into water immediately behind the rack. Proximity improves heat-exchanger effectiveness;

- Trade-offs are higher rack-level capex, more moving parts and potentially higher fan power. In mixed deployments, a CDU may be added for liquid control.

- RDHx and DLC can coexist in the same deployment;

<br>

## 3. Liquid cooling: the architecture to understand

### Direct-to-Chip Liquid Cooling (DLC)

- DLC places a cold plate directly on high-heat components such as CPUs and GPUs. Liquid carries heat away far more efficiently than moving the same heat through room air.

- SemiAnalysis used the GB200 NVL72 (~120 kW rack) as the inflection point that brought DLC deployments into mainstream AI infrastructure discussion.

- DLC does not necessarily cool every component. Memory, networking, power electronics or other components may still rely partly on air, so liquid-cooled racks can still require airflow.

### The liquid path

| **Layer** | **Typical components** | **Role** | **Key distinction** |
| --- | --- | --- | --- |
| **IT / rack loop** | Cold plates, hoses, manifolds, quick disconnects | Collect heat directly from components. | Closest to sensitive electronics; cleanliness, leak management and pressure control are critical. |
| **CDU** | L2L heat exchanger, pumps, controls | Transfers heat between the IT loop and facility loop while controlling flow / temperature / pressure. | Creates hydraulic and fluid-quality separation between the two circuits. |
| **Facility water loop** | Pumps, piping, headers | Moves heat across the building to heat rejection. | May serve both liquid-cooled IT and other cooling equipment. |
| **Heat rejection** | Chiller, dry cooler, cooling tower, economiser | Rejects heat to the ambient environment. | DLC changes where heat is captured; it does not remove the need to reject that heat. |

### CDU in plain English

- A CDU is the interface between the data-center facility and liquid-cooled IT.

- Core components are a liquid-to-liquid heat exchanger, pumps and control electronics.

- It manages coolant flow rate, pressure drop and temperature, and can isolate IT coolant chemistry from facility water.

- SemiAnalysis notes CDU capacities commonly above 1 MW, with many architecture variants.

### What the 2025 report does - and does not - establish

- It establishes the structural direction: rising AI density increases the value of moving cooling closer to the chip.

- It does not establish that all future data centers become fully liquid-cooled, or that air cooling disappears.

- The report's detailed discussion of L2L, L2A, immersion and two-phase cooling sits behind the paid section in the uploaded source; this note therefore does not invent conclusions that are not supported by the accessible material.

<br>

## 4. Chillers and heat rejection

| **System** | **How heat is rejected** | **Strength** | **Trade-off** |
| --- | --- | --- | --- |
| **Water-cooled chiller + cooling tower** | Refrigerant → condenser water → evaporative cooling tower | Very large unit capacity and high energy efficiency. | High water use; more piping, pumps and water treatment. |
| **Air-cooled chiller** | Refrigerant condenser rejects heat directly to outside air with fans | Simpler system and low water use. | Lower per-unit capacity and generally lower efficiency in hot conditions. |
| **Dry cooler** | Closed-loop water/glycol coil rejects heat to outdoor air | No evaporative water loss. | Performance depends strongly on ambient dry-bulb temperature; fan area can be large. |
| **Adiabatic dry / air-cooled system** | Evaporative pre-cooling lowers incoming air temperature before heat rejection | Hybrid compromise between water and energy use. | Still consumes some water and benefit falls in humid conditions. |
| **Economiser / free cooling** | Outside air or water conditions bypass / reduce compressor use | Can materially lower PUE and operating cost. | Highly dependent on climate and allowable IT inlet temperatures. |

### Chiller basics

- A chiller is essentially a large refrigeration machine. Its key components include an evaporator, compressor, condenser and expansion valve.

- The compressor is the major energy-consuming component; reducing the required temperature lift lowers compressor work.

- The report cites large water-cooled chillers at roughly 15-20 MW cooling capacity per unit, versus air-cooled units around ~2 MW at the high end of the example shown.

- Chiller capacity is often quoted in refrigeration tons (RT): 1 RT ≈ 3.517 kW of cooling.

### Energy vs. water trade-off

- Evaporative cooling can reduce compressor energy by exploiting the wet-bulb temperature, especially in hot and dry climates.

- The same mechanism consumes water. This is why a low-PUE design can still have high WUE.

- Climate is therefore part of the cooling architecture: hot/humid locations are much harder for free cooling than cool or dry locations.

<br>

## 5. Hyperscaler design lessons from the report

| **Operator / design** | **Cooling approach highlighted in the report** | **Industry lesson** |
| --- | --- | --- |
| **Microsoft** | Airside free cooling / direct evaporative cooling in suitable climates; indirect evaporative variants elsewhere. | **Avoiding chillers** can lower capex and energy use, but water use can rise sharply in hot/dry locations. |
| **Meta legacy 'H'** | Free cooling, high server inlet temperature and low rack density. | **Excellent PUE/WUE** can come at the cost of lower density and slower buildout. |
| **Google** | Heavy use of waterside economisers and evaporative cooling towers; some chillerless sites. | Very low PUE can be achieved with higher water consumption - a clear energy/water trade-off. |
| **AWS** | Report infers substantial use of outside-air / free-cooling-style designs from site observations. | Hyperscalers standardise around internal workloads and can optimise more aggressively than multi-tenant colo operators. |

## 6. Essential terms

| **Term** | **Meaning** |
| --- | --- |
| **DLC** | Direct-to-Chip Liquid Cooling: cold plates remove heat directly from high-power components. |
| **RDHx** | Rear-Door Heat Exchanger: water-cooled radiator on the rack exhaust; servers themselves remain air-cooled. |
| **CDU** | Coolant Distribution Unit: interface between IT coolant and facility water. |
| **L2L** | Liquid-to-Liquid heat exchange; one liquid loop transfers heat to another without mixing fluids. |
| **CRAC** | Computer Room Air Conditioner; local refrigeration-based room cooling. |
| **CRAH** | Computer Room Air Handler; room air handler using central facility chilled water. |
| **Fan Wall** | Large, high-capacity bank of fans / coils serving a data hall. |
| **Chiller** | Mechanical refrigeration equipment that lowers water / coolant temperature. |
| **Cooling Tower** | Rejects heat from condenser water, commonly using evaporation. |
| **Dry Cooler** | Closed-loop heat rejection to outdoor air without evaporative water loss. |
| **Economiser / Free Cooling** | Uses ambient air or water conditions to reduce or bypass mechanical refrigeration. |
| **Delta T** | Temperature rise across a load or heat exchanger; a larger useful Delta T can reduce required flow. |
| **PUE** | Power Usage Effectiveness = total facility power / IT power. |
| **WUE** | Water Usage Effectiveness = water use per unit of IT energy. |

---

[上一篇：电力与电气基础](../foundations/01-power-and-electrical-basics.md) · [下一篇：为什么转向800VDC](../800vdc/03-why-800vdc.md)
