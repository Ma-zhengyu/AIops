# Experiments To Build Next

这个目录先作为后续动手项目占位。建议做 4 个小项目，逐步拼成一个面向汽车/制造业的 AIOps portfolio。

## 1. Time-Series Anomaly Detection

数据：SMD、SMAP/MSL、NASA turbofan 或自造设备传感器数据。  
方法：STL/MAD、Isolation Forest、LSTM-AE、OmniAnomaly 思路。  
输出：异常区间、异常维度贡献、检测延迟、误报分析。

## 2. Log Intelligence

数据：Loghub HDFS/BGL/OpenStack。  
方法：Drain 解析、模板序列统计、DeepLog/LogAnomaly 类模型、LLM 摘要。  
输出：日志模板、异常日志片段、候选原因解释。

## 3. Graph RCA

数据：mock 微服务拓扑或 AIOps Challenge 2020。  
方法：服务拓扑 + 指标异常 + 变更事件 + 随机游走/PageRank。  
输出：top-k 根因、证据链、可解释诊断报告。

## 4. SRE-Copilot Prototype

输入：一条告警或事故描述。  
工具：查指标、查日志、查拓扑、查 Runbook、生成诊断报告。  
输出：事故摘要、影响面、根因候选、下一步动作、风险提醒。

## 最终作品集形态

建议最终合并成一个 demo：

- `observability-stack/`：Prometheus + Grafana + OpenTelemetry。
- `data-pipeline/`：Kafka/Flink/ClickHouse 或简化版。
- `models/`：异常检测、日志解析、RCA 排序。
- `agent/`：SRE-Copilot。
- `docs/demo-report.md`：从告警到诊断的完整样例。

