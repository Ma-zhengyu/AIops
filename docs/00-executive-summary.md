# AIOps 调研总览

## 一句话判断

AIOps 的成熟形态不是一个“异常检测模型”，而是一套围绕生产系统可靠性的智能闭环：采集可观测数据，建立统一语义，检测异常，定位根因，推荐/执行缓解动作，并把事故经验沉淀回知识库、模型和平台。

## 通用互联网/云原生 AIOps 发展到哪里了

学术界已经把单点任务研究得比较深：日志解析与日志异常检测、时间序列异常检测、多变量指标建模、微服务根因定位、事故工单聚类、事故摘要和分派。代表性工作包括 DeepLog、LogAnomaly、LogRobust、OmniAnomaly、Microsoft 的 KDD 2019 时间序列异常检测服务、Narya、CloudRanger、MicroRCA 等。

产业界比学术界更重视闭环和落地约束。Microsoft、Meta、IBM、Datadog、Dynatrace、Splunk、Grafana 等都把 AIOps 与可观测性、事故管理、LLM copilot、自动化运维结合。Microsoft Azure 2025 年公开的 Triangle System 已经把多 Agent 用在事故初始分派；Meta 2024 年公开了“启发式检索 + LLM 排序”的代码变更根因辅助系统。

通用场景的成熟度可以粗略分为四层：

1. 监控自动化：Prometheus/Grafana/ELK/Tracing/OTel。
2. 智能告警：动态阈值、异常检测、告警降噪、事件聚合。
3. 智能诊断：拓扑/链路/日志/指标/变更结合做 RCA。
4. 智能处置：Copilot、Runbook 自动化、多 Agent 协作和受控自愈。

目前行业正在从第 2、3 层向第 4 层走，但真正“无人值守自愈”仍受限于误报、责任归属、权限、安全和变更风险。

## 制造业/汽车 AIOps 发展到哪里了

制造业论文通常不用 AIOps 这个词，而是使用 Predictive Maintenance、PHM、Smart Manufacturing、Industrial IoT、Digital Twin、Real-time Anomaly Detection、Quality Analytics 等术语。研究主线包括设备预测性维护、产线 KPI 异常检测、工艺质量异常、设备健康评分、剩余寿命预测、工业传感器时序建模和可解释诊断。

汽车方向有两条线：

1. 制造侧：冲压、焊装、涂装、总装、电池、电驱、仓储物流等产线的预测性维护、质量根因分析、产能瓶颈识别。
2. 车辆/车云侧：车端故障诊断、远程健康监测、OTA 与云服务稳定性、智能座舱/智驾数据平台、车联网数据链路、模型训练/推理基础设施运维。

制造业和汽车 AIOps 的特殊性在于：异常不是只影响 QPS 或延迟，还可能造成停线、返修、质量波动、安全风险和供应链扰动。模型必须能解释、能和专家规则共存、能在数据缺标注和工况漂移下稳定工作。

## 理想汽车岗位画像

公开校招岗位信息显示，该岗位关注 AIOps 前沿算法工程化、运维数仓、数据清洗/特征工程/ETL/数据图谱、SRE-Copilot、multi-agent、智能诊断、故障预测、运维大模型训练微调、Agent Framework/Runtime、Browser/Code Interpreter 沙箱和 Agent 可观测性。

这意味着它不是传统“运维工程师”，也不是纯算法研究岗，而是算法、数据平台、云原生、SRE 和 LLM Agent 的交叉岗位。你需要既能读论文，也能把模型放进真实生产流程。

## 未来 3-5 年方向

最值得提前布局的方向：

1. LLM4AIOps：事故摘要、工单分派、Runbook 问答、根因候选排序、修复建议。
2. Multi-agent SRE：不同团队/系统/工具的 Agent 协作，但要有人类审批和可追溯。
3. Causal + Graph RCA：从相关性走向因果、拓扑、变更、知识图谱融合。
4. Observability Data Lake：日志、指标、链路、事件、变更、工单的统一数据底座。
5. AI/LLM Observability：未来 AIOps 还要反过来运维 AI 系统本身，包括 Agent、RAG、训练/推理平台。
6. Industrial AIOps：IT/OT 融合、数字孪生、预测性维护、质量根因分析、工业知识图谱。

## 入职前优先级

前三个月建议围绕“能上手真实任务”安排：

1. 用 Python/PyTorch/scikit-learn 做时间序列异常检测和日志异常检测复现。
2. 用 Prometheus + Grafana + OpenTelemetry + ClickHouse/Elastic 搭一个可观测性小系统。
3. 用 Kafka/Flink/Spark/Airflow/ClickHouse 做一个运维数仓样例。
4. 用 Neo4j 或 NetworkX 做服务拓扑 + 告警传播 + RCA 排序。
5. 用 LangChain/LangGraph/AutoGen 做 SRE-Copilot 原型：输入告警、拉日志、查知识库、输出诊断报告。
6. 补工业知识：MES/SCADA/PLC/OPC UA、预测性维护、数字孪生、质量工程、FMEA。

