# AIOps Research for Automotive/Manufacturing Context

调研日期：2026-04-25  
目标：为入职理想汽车 AIOps 算法工程师前的长期学习与技术判断建立一个本地研究仓库。

## 仓库结构

- `docs/00-executive-summary.md`：一页式总览，适合快速复盘。
- `docs/01-general-aiops.md`：通用互联网/云原生 AIOps 调研。
- `docs/02-manufacturing-automotive-aiops.md`：制造业、汽车、工业现场相关 AIOps/智能运维调研。
- `docs/03-academia-industry-future.md`：学术界、产业界成熟度与未来方向。
- `docs/04-li-auto-skill-roadmap.md`：面向理想汽车 AIOps 岗位的技能路线。
- `data/sources.md`：权威资料、论文、产业文章索引。
- `data/paper_matrix.csv`：论文/资料结构化表格。
- `experiments/README.md`：后续可以动手复现实验的建议。
- `templates/paper-note.md`：读论文笔记模板。

## 核心结论

AIOps 已经从“把监控数据接进机器学习模型”发展到“围绕 SRE 工作流重构自动化闭环”。通用云原生场景的主线是日志、指标、链路、工单、变更记录的统一建模，然后做异常检测、告警降噪、根因定位、事故分派、修复建议和部分自动缓解。

制造业/汽车场景不是把互联网 AIOps 原样搬过去。它更接近“IT + OT + 物理资产”的融合：产线设备、PLC/SCADA/MES、质量检测、供应链、车云服务、OTA、座舱/智驾数据平台都可能进入运维闭环。核心难点从单纯的服务可用性，扩展到安全、质量、停线成本、实时性、可解释性、跨工厂迁移和专家知识沉淀。

对理想汽车 AIOps 算法工程师而言，最值得建立的护城河是：

1. 可靠性/SRE 语境下理解业务指标、SLO、事故生命周期。
2. 运维数仓、特征工程、指标体系、血缘和图谱能力。
3. 时间序列异常检测、日志智能、RCA、因果/图模型。
4. 云原生工程化：Kubernetes、可观测性、服务治理、流批一体。
5. LLM/RAG/Multi-agent 在 SRE-Copilot 和 AgentOps 中的落地能力。
6. 面向制造业的工业数据、预测性维护、数字孪生、质量与安全知识。

## 建议使用方式

先读 `docs/00-executive-summary.md`，再按你未来岗位优先读 `docs/04-li-auto-skill-roadmap.md`。如果要做作品集或入职前项目，直接看 `experiments/README.md`。

