# AI 可观测 / AIOps / LLMOps 面经库

## 岗位画像
- 国内没有"LLM Observability Engineer"这个头衔，藏在四类 JD 下：①AIOps/基础设施可观测（字节/阿里云/腾讯）；②LLMOps/大模型评测（腾讯大模型应用岗；**字节大模型评测工程师 2027 届校招——本方向少见的校招口**）；③AI Agent 平台（美的/小赢/京东）；④云厂商可观测产品线（阿里云 ARMS/SLS，30-50K·16，本科+1-3 年；2025 届起招实习）。
- **转型岗特征：基本不招纯应届**，主力是 3-6 年后端/SRE/可观测工程师转型；共同底线="扎实后端功底（Go/Java）+已补上 LLM 层知识"。
- 技能四件套：①三支柱+**OpenTelemetry**+Prometheus/Grafana/ELK（eBPF 加分）；②Go/Java；③K8s/云原生；④LLM 特有指标——token 用量/延迟/单查询成本/幻觉与评测跟踪/漂移检测+向量库与 RAG 生态。
- 面试特征：**基本不考 LeetCode hard，考"你搭过什么、坏了怎么查"**。

## 面试流程（社招为主）
一轮可观测八股+排障场景 → 二轮系统设计（监控体系/告警体系）→ 主管面看平台工程经验。

## 真题库

### 八股
1. **可观测三大支柱 Metrics/Logging/Tracing 各回答什么问题？如何用 TraceID 串联？采样策略头部 vs 尾部怎么选？**（高德/陌陌实践衍生；SRE 题库——头部采样省成本但会漏错误，尾部采样保错误与慢请求、实现重）
2. Prometheus 架构、Pull vs Push、四种指标类型（Counter/Gauge/Histogram/Summary）、**rate()/histogram_quantile() 怎么算 P99**、TSDB 原理、Thanos/VictoriaMetrics 高可用（高频）
3. OpenTelemetry：三大信号、OTLP、Collector 的 receiver/processor/exporter、W3C Trace Context 透传（知识点清单；原题样本少）
4. AIOps 落地路径：**先告警降噪→再根因分析→后异常预判**（腾讯云/代码川；阿里云智能运维岗 JD 直接列明：时序异常检测、日志聚类、根因定位、变更风险预测）
5. 大模型评测（LLMOps 线）：评测基准怎么选、**LLM-as-judge 的偏差**、离线评测 vs 在线 A/B（字节/阿里/快手/腾讯真题——小林 note 收录）

### 系统设计
1. **"如何为公司构建监控体系"**：指标 Prometheus+Grafana、日志 EFK、链路 SkyWalking/Jaeger、TraceID 驱动排障（腾讯云 SRE 对照表）
2. **"如何避免告警疲劳"**：分层告警（P0-P3）、基于 SLO 的告警（错误预算消耗过快才触发）、告警收敛与去重（80wz 题库）
3. SkyWalking 落地细节：Agent 无侵入埋点、采样、存储调优、告警联动（CSDN 2026 实战考点）
4. 设计 Claude 安全评估基础设施（实时+批量分类器）、大规模多租户沙箱（Anthropic 方向）
5. 机试：带 TTL/压缩/并发的 in-memory DB 或任务调度器（CodeSignal 90 分钟）

### 项目深挖
1. 异常检测算法选型（3-sigma/EWMA/孤立森林/LSTM-VAE）与**误报率指标**、根因定位如何缩短 MTTT（美团 AIOps 实践衍生）
2. LLM 应用可观测项目：token 成本归因、trace 覆盖率、评测门禁怎么做（新兴追问）

## 重点题答题要点

**监控体系设计四层模板**（系统设计万能框架）：
① **采集**：OTel 统一探针，三大信号+LLM 专属 span（模型调用/工具调用/检索各有属性）；
② **传输存储**：OTLP→Collector（尾部采样：错误全采+正常抽样）→TSDB/对象存储；基数（cardinality）治理要主动提；
③ **消费**：SLO 看板、告警分级、TraceID 串联三支柱排障；
④ **LLM 新增层**：token 用量/延迟分位（TTFT、TPOT）/单查询成本/评测通过率/输出漂移——**把"传统三支柱+LLM 四指标"讲全，就是与老 SRE 的差异化**，也是"转型岗"考官最想听的一层。

**告警体系**：SLO 定义（可用性/延迟目标）→ 错误预算 → 预算消耗速率告警（而非单点阈值）→ 分级路由（P0 电话/P3 工单）→ 收敛（同因聚合、静默窗口）。

**采样策略**：头部采样在 SDK 端决定（省资源但错误可能被丢）；尾部采样在 Collector 看完整 trace 再决定（保留所有错误+慢请求，代价是全量上报到 Collector）——生产常见组合：头部粗筛+尾部精筛。

**P99 计算**：Histogram 按桶累计，`histogram_quantile(0.99, rate(http_request_duration_seconds_bucket[5m]))`——要能解释桶边界插值与为什么不用 Summary（不能聚合跨实例）。

## 挂人点
① 只会"装过 Prometheus"，讲不出采样与基数爆炸治理；② 告警设计没有 SLO/错误预算概念；③ 对 LLM 指标（token/成本/评测）零认知——这正是"转型岗"与"老 SRE"的分界线；④ 讲排障流程没有 TraceID 串联的完整链路故事；⑤ 系统设计漏掉"数据本身的管理"（留存策略/脱敏/成本）。
