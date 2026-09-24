# 原文文件、链接与对应笔记

[返回学习目录](README.md)

| 原文 | 日期/版本 | 文件与链接 | 对应笔记 |
| --- | --- | --- | --- |
| Datacenter Anatomy Part 1: Electrical Systems | 2024-10-14 | [HTML归档](references/semianalysis-datacenter-anatomy-1-electrical.html) · [原文网站](https://newsletter.semianalysis.com/p/datacenter-anatomy-part-1-electrical) | [01 · 对应笔记](notes/foundations/01-power-and-electrical-basics.md) |
| Datacenter Anatomy Part 2 – Cooling Systems | 2025-02-13 | [HTML归档](references/semianalysis-datacenter-anatomy-2-cooling.html) · [原文网站](https://newsletter.semianalysis.com/p/datacenter-anatomy-part-2-cooling-systems) | [02 · 对应笔记](notes/foundations/02-cooling-system-basics.md) |
| Inside the 800VDC Revolution – Part 1 | 2026-05-26 | [HTML归档](references/semianalysis-800vdc-revolution-part-1.html) · [原文网站](https://newsletter.semianalysis.com/p/inside-the-800vdc-revolution-part) | [05 · 对应笔记](notes/industry/05-semianalysis-transition.md) |
| NVIDIA — 800 VDC Architecture for Next-Generation AI Infrastructure | 2025-10 | [PDF](references/nvidia-800vdc-architecture-v1.pdf) · [原文网站](https://www.nvidia.com/en-us/data-center/technologies/800-vdc-architecture/) | [04 · 对应笔记](notes/800vdc/04-nvidia-v1-architecture.md) |
| Oxcap — 800V DC Datacenter Transition | 2026-06-02 | [PDF](references/oxcap-800vdc-transition-2026-06-02.pdf) · [出版方网站](https://oxcapanalytics.com/) | [06 · 对应笔记](notes/industry/06-oxcap-june-transition.md) |
| Oxcap — ABB/Legrand CMDs and the 800V DC debate: Asking the right questions | 2026-09-22 | [PDF](references/oxcap-800vdc-cmd-debate-2026-09-22.pdf) · [出版方网站](https://oxcapanalytics.com/) | [07 · 对应笔记](notes/industry/07-oxcap-september-cmd.md) |
| SemiAnalysis — Stop Saying Half of 2026 US Datacenter Capacity Is Canceled | 2026-06-18 | [PDF](references/semianalysis-us-datacenter-capacity-2026-06-18.pdf) · [原文网站](https://newsletter.semianalysis.com/p/stop-saying-half-of-2026-us-datacenter) | 新增建设与容量研究资料；尚未单独整理笔记 |

03是综合多份资料形成的个人逻辑整理，主要衔接NVIDIA第一版、SemiAnalysis的迁移框架及下面的补充资料。06和07分别对应Oxcap六月与九月的两篇报告。

## 归档说明

- 四份PDF按提供的文件原样归档，包括补齐的Oxcap六月原文；重复副本只保留一份。
- 三份HTML归档保留保存文件中已有的文章正文、表格和图片引用，移除网页脚本及站点界面，修复失效的本地图片路径。图片仍引用原网站，需要联网；HTML可下载后用浏览器打开。
- 已保存的HTML不包含付费墙后未保存的内容，归档未补充这些部分。
- NVIDIA官网入口可能随版本更新；仓库中的第一版PDF是固定版本。
- Oxcap链接是出版方主页；具体报告请打开对应PDF。
- [文件校验与整理记录](references/manifest.json)记录原文件名、SHA-256、版本与对应关系。

## 03个人综合笔记中的补充链接

- [NVIDIA：800 VDC Power Architecture / AI Factory](https://blogs.nvidia.com/blog/800-vdc-power-architecture-ai-factory/)
- [NVIDIA Developer：原笔记引用的技术文章](https://developer.nvidia.com/blog/?p=100571)
- [NVIDIA NVL72 AI Factory参考架构：Components](https://docs.nvidia.com/enterprise-reference-architectures/nvl72-ai-factory/latest/components.html)
- [OCP：Power Architecture Evolution in Data Centers](https://www.opencompute.org/documents/power-architecture-evolution-in-data-centers-pdf)

## 已记录的核对事项

- 03：机柜功率分段为解释框架，不是硬性行业标准；电压与损耗比较须保留假设。
- 04：导体利用率比较有特定配置前提；个人补充中的变压器年龄与余量数字缺少明确来源，不宜直接用于建模。
- 05：技术时间表、sidecar与SST市场规模、单价和节能幅度是2026年5月报告估计，不能当作已经发生的结果。
- 06：厂商相对判断属于2026年6月的报告观点，需结合后续产品与业务变化更新。
- 07：九月Oxcap原文的2030年SST规模出现约130亿美元与约320—324亿美元两组数字；容量和效率描述也有口径不一致。详细记录见该笔记，定量使用前需回到原始模型核对。

各Markdown笔记正文保留原有语言和论证；中文阅读定位与本仓库导读用于串联逻辑。
