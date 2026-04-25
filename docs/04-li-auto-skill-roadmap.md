# 面向理想汽车 AIOps 算法工程师的学习路线

## 岗位拆解

公开岗位描述可以拆成五块：

1. AIOps 前沿算法研究与工程化落地。
2. 运维数仓：数据清洗、特征工程、ETL、数据图谱。
3. SRE-Copilot：multi-agent、智能诊断、故障预测、运维大模型训练微调。
4. AgentCore：Agent Framework、Agent Runtime、Browser/Code Interpreter 沙箱、Agent 可观测性。
5. 云原生/平台工程：Docker、Kubernetes、Helm、Istio、Envoy、gRPC、Prometheus、Grafana、ELK/EFK、CI/CD。

所以你要准备的是“T 型能力”：算法深度 + 工程广度 + 工业/汽车场景理解。

## 第一优先级：必须能上手

### Python 与算法工程

目标水平：能独立完成数据处理、模型训练、评估、服务化和实验记录。

要掌握：

- Python 数据栈：pandas、numpy、polars、pyarrow。
- 机器学习：scikit-learn、XGBoost、LightGBM。
- 深度学习：PyTorch，至少熟悉 Dataset/DataLoader、训练循环、保存加载、GPU 调试。
- 模型评估：precision/recall/F1、PR-AUC、ROC-AUC、top-k、延迟、吞吐、漂移。
- 工程规范：类型标注、日志、配置管理、单元测试、Docker 化。

### 时间序列异常检测

目标水平：能解释并复现 3 类方法，能根据业务数据选择 baseline。

要掌握：

- 统计方法：滑动窗口、EWMA、STL、MAD、季节性分解、动态阈值。
- 传统 ML：Isolation Forest、LOF、One-Class SVM、PCA。
- 深度模型：LSTM-AE、VAE、TCN、Transformer、OmniAnomaly 思路。
- 工业注意点：延迟检测、连续异常合并、冷启动、周期变化、数据缺失。

### 日志智能

目标水平：能从原始日志到异常检测完成端到端 pipeline。

要掌握：

- 日志解析：Drain、Spell 思路。
- 模板序列建模：DeepLog、LogAnomaly、LogRobust。
- 文本语义：embedding、sentence-transformers、LLM 日志摘要。
- 生产问题：日志模板演进、噪声、采样、字段规范、敏感信息脱敏。

### RCA 与图建模

目标水平：能把服务拓扑、指标异常、变更事件融合成根因候选排序。

要掌握：

- 图基础：NetworkX、Neo4j、PageRank/随机游走、社区发现。
- 微服务 RCA：CloudRanger、MicroRCA、因果发现基本概念。
- 知识图谱：实体/关系设计、指标血缘、服务依赖、告警本体。
- 解释输出：为什么这个节点是候选根因，证据来自哪些指标/日志/变更。

## 第二优先级：工程落地能力

### 云原生与可观测性

目标水平：能看懂生产 Kubernetes 系统，能搭建可观测 demo。

要掌握：

- Docker、Kubernetes、Helm。
- Prometheus、Grafana、Alertmanager。
- OpenTelemetry、Jaeger/Tempo。
- ELK/EFK、Loki。
- Istio/Envoy/gRPC 基础。
- SLO、SLI、错误预算、事故响应流程。

### 数据平台

目标水平：能设计运维数仓的 ODS/DWD/DWS/ADS 分层，能做指标血缘。

要掌握：

- Kafka：事件接入。
- Flink：实时清洗、窗口、CEP。
- Spark：离线 ETL。
- Airflow：任务编排。
- ClickHouse：时序/日志分析。
- Hudi/Delta Lake：湖仓、增量。
- Neo4j：图谱。
- 数据质量：唯一性、完整性、及时性、口径一致性。

## 第三优先级：LLM/Agent

### RAG 与运维知识库

目标水平：能做一个可评估的 Runbook/事故复盘问答系统。

要掌握：

- 文档切分、embedding、向量库、BM25 + dense 混合检索。
- reranker、引用溯源、答案置信度。
- 知识更新、过期文档识别。
- 运维问答评估：答案正确性、可执行性、引用准确性。

### Multi-agent SRE-Copilot

目标水平：能做一个最小闭环原型。

建议 Agent 设计：

- Triage Agent：判断事故类型、影响范围、优先级。
- Metrics Agent：查询指标并判断异常区间。
- Logs Agent：检索日志、聚类错误、摘要异常。
- Topology Agent：查询依赖图和变更图。
- RCA Agent：融合证据输出 top-k 根因。
- Action Agent：匹配 Runbook，生成候选动作。
- Reviewer Agent：检查风险、权限、回滚方案。

### 运维大模型微调

目标水平：了解 LoRA/QLoRA/PEFT，能做小规模指令微调，但更重视数据构造和评估。

重点不是盲目训练大模型，而是：

- 构造事故问答、摘要、分派、根因排序数据。
- 做偏好数据和人工反馈。
- 评估幻觉、误导、引用错误、越权建议。
- 设计 human-in-the-loop 流程。

## 制造业/汽车补课清单

### 工业基础

目标水平：能和设备/工艺/质量工程师对话。

要了解：

- MES、SCADA、PLC、OPC UA、工业网关。
- OEE、节拍、良率、停线、Andon、瓶颈工位。
- FMEA、SPC、8D、5Why、鱼骨图。
- 预测性维护、PHM、RUL、CBM。
- 数字孪生、资产层级、工艺路线、批次追溯。

### 汽车基础

目标水平：知道智能汽车公司 AIOps 为什么复杂。

要了解：

- OTA、车云链路、车端日志、DTC/OBD。
- 智能座舱服务、语音/多模态交互指标。
- 智驾数据闭环：采集、回传、标注、训练、仿真、评测。
- AI 基础设施：GPU 集群、训练任务、数据湖、模型服务、推理监控。

## 12 周入职前路线

### 第 1-2 周：SRE 与可观测性

- 读 Google SRE 的 SLO、监控、事故响应章节。
- 搭建 Prometheus + Grafana + OpenTelemetry demo。
- 输出：一个服务的 SLI/SLO 设计文档。

### 第 3-4 周：时间序列异常检测

- 复现 STL/MAD、Isolation Forest、LSTM-AE。
- 用 SMD 或 NASA/SMAP/MSL 数据做实验。
- 输出：异常检测实验报告，比较延迟、F1、误报。

### 第 5-6 周：日志智能

- 跑 Drain + DeepLog/LogAnomaly 类 pipeline。
- 用 Loghub HDFS/BGL 数据做异常检测。
- 输出：日志解析、模板统计、异常解释报告。

### 第 7-8 周：RCA 与图谱

- 构建一个 mock 微服务拓扑。
- 模拟指标异常、依赖传播和变更事件。
- 用 PageRank/随机游走/规则融合输出 top-k 根因。
- 输出：RCA demo 和可解释诊断报告。

### 第 9-10 周：SRE-Copilot 原型

- 用 RAG 接入 Runbook/事故复盘。
- 加工具调用：查指标、查日志、查拓扑。
- 输出：输入告警后自动生成事故摘要、证据链、候选根因、建议动作。

### 第 11-12 周：制造业/汽车化改造

- 把 demo 的实体改成工厂/产线/设备/工位/质量/维修。
- 加入预测性维护样例和数字孪生/资产图。
- 输出：面向汽车制造 AIOps 的作品集 README。

## 你要达到的“能说清楚”

面试或入职初期，你最好能清楚回答：

1. 为什么异常检测不能只看 F1？
2. 如何设计运维数据模型和指标血缘？
3. 日志、指标、链路、变更如何融合做 RCA？
4. LLM 在 AIOps 中适合做什么，不适合做什么？
5. Multi-agent SRE-Copilot 如何防止误操作？
6. 制造业预测性维护为什么需要可解释性？
7. 汽车公司里的 AIOps 和互联网公司有什么不同？

