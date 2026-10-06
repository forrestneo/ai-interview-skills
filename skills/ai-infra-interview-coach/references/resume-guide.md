# 简历优化指南：按岗位 JD 要求改简历

> 配合目标岗位的 reference 使用：本文件给方法与公式，方向文件给关键词清单和深度标尺。核心认知：**简历筛选 = 关键词匹配（HR/系统初筛）+ 证据评估（面试官复筛）**。两关都要过。

## 一、简历结构（AI 基础设施类岗位标准模板）

```
① 基本信息：姓名/联系方式/GitHub（有 PR 或项目必放）/求职意向（写到方向粒度：不是"AI Infra 工程师"，是"大模型推理优化工程师"）
② 技能清单：按 JD 关键词分层写，用动词不用形容词——"vLLM（改过 Scheduler 调度逻辑）"而不是"精通 vLLM"
③ 项目/实习经历（简历主体，占 60%+ 篇幅）：每条 = 动作 + 技术词 + 量化结果
④ 开源/竞赛/论文（如有）：PR 写明仓库与内容；Kaggle 写名次与百分位
⑤ 教育背景：放最后（应届可前置）；校招硕士是事实门槛，学历好就放前
```

篇幅：应届/3 年内一页；资深两页封顶。与目标方向无关的经历压缩到一行或删除。

## 二、改写公式与四级深度标尺

**经历条目公式**：`[做了什么动作] + [用了什么技术（JD 原词）] + [量化结果（从 X 到 Y / 规模 N / 比例 %）] + [怎么测的（一句话，放追问弹药位）]`

**技能四级标尺**（写简历前先自测，防面试打穿）：
| 级别 | 简历可写 | 示例表述 |
|---|---|---|
| L1 用过 | "使用/熟悉" | 使用 vLLM 部署 7B 模型 |
| L2 调优过 | "调优/排查" | 通过调 continuous batching 参数将吞吐提升 X% |
| L3 改过源码 | "二次开发/修改" | 定位 vLLM Scheduler 前置阻塞问题并修改调度逻辑 |
| L4 贡献过 PR | "贡献者" | 向 vLLM 提交 XX 修复 PR（已合并） |

夸大一级就会在二面被打穿（写 L3 会被追问源码细节）；做过 L2 只写 L1 是浪费——**如实但顶格写**。

**改写示例（before → after）**：
- ❌ "负责大模型推理服务，性能良好" → ✅ "基于 vLLM 部署 Qwen-72B 推理服务；定位 decode 阶段 KV cache 碎片问题，启用 prefix caching + 调整 gpu_memory_utilization，长会话场景 TTFT 从 1.8s 降至 0.6s（压测：并发 50，200 组真实对话回放）"
- ❌ "参与数据清洗工作" → ✅ "构建预训练数据清洗管线（datatrove+Ray，日均处理 X TB）：MinHash+LSH 去重（文档级去重率 X%）、质量分类器过滤（丢弃率 X%）；消融实验显示清洗后小模型 proxy 评测提升 X 分"
- ❌ "熟悉 Kubernetes" → ✅ "开发 GPU 配额管理组件（Go，K8s Operator 模式）：支持部门级配额借还与优先级抢占，集群 GPU 利用率从 31% 提升至 68%（利用率按 SM 活动率口径统计）"

## 三、七大方向的 JD 高频词清单（关键词对照用）

**训练方向**：Megatron-LM / DeepSpeed / FSDP / ZeRO-1/2/3 / TP·PP·DP 并行 / 3D 并行配比 / NCCL / RDMA / BF16·FP8 / 混合精度 / MFU / loss spike / checkpoint 容错 / 万卡集群 / MoE 专家并行 / FlashAttention
**推理方向**：vLLM / SGLang / TensorRT-LLM / PagedAttention / KV cache / Continuous Batching / 量化（GPTQ/AWQ/FP8/SmoothQuant）/ CUDA / Triton / PD 分离 / 投机解码（EAGLE/Medusa）/ TTFT / 吞吐 / prefix sharing / CUTLASS
**容器调度**：Kubernetes（调度器/设备插件/Operator）/ Go / Volcano / Kueue / gang scheduling / GPU 共享（MIG/HAMi/vGPU）/ 配额管理 / 超卖 / 利用率 / Ray / Slurm / cgroups
**Data Infra**：C++ / Rust / LSM-Tree / B+树 / MVCC / 向量化执行 / SIMD / 查询优化器 / ClickHouse / Doris / StarRocks / MergeTree / Flink（Checkpoint/Watermark）/ Spark / Iceberg / Hudi / Kafka / HNSW / IVF / PQ / Milvus / RAG 管线
**大模型数据**：数据配比 / 课程学习 / MinHash / LSH / SimHash / 质量过滤 / reward model 打分 / LLM-as-judge / 合成数据 / 蒸馏 / SFT / LoRA / QLoRA / RLHF / DPO / 评测集构建 / datatrove / Spark / Ray / scaling law
**多模态**：CLIP / InfoNCE / 对比学习 / BLIP / Q-Former / Qwen-VL / LLaVA / InternVL / OCR / 图文对 / visual grounding / 视频理解 / perceptual hash / 标注体系 / Kappa 系数 / DDPM / 扩散 / 具身数据 / 遥操作
**AI 可观测**：OpenTelemetry / OTLP / Prometheus / Grafana / 三支柱（Metrics/Logging/Tracing）/ TraceID / 采样策略 / SLO / 错误预算 / 告警收敛 / eBPF / SkyWalking / token 用量 / TTFT·TPOT / 评测门禁 / 漂移检测 / LLM-as-judge

**模型公司专属加分词（DeepSeek/Kimi/MiniMax/智谱/通义，2026-10 实测 JD）**：Vibe Coding 重度用户 / 深度使用 Claude Code·Manus·Cursor（写成工作流条目）/ MCP / Tool Use / Function Calling / 跨 session 记忆连续性 / 可验证环境 / GUI Agent / Computer-Use / MicroVM·沙箱隔离（Firecracker/EROFS）/ Agent 任务监控 / 多 LoRA / PTU 推理工具链 / Lightning Attention（面 MiniMax 必备）/ 开源生态维护（HuggingFace/ModelScope）

用法：目标 JD 拿到后，把 JD 里的词与上表比对——简历里必须出现 JD 原词（"KV cache"别写成"缓存优化"），但每个出现的词都要过四级标尺自测。**投模型公司时额外做一件事：把"重度使用 AI 工具"写成独立条目**（例："基于 Claude Code+自建脚本构建代码审查工作流，团队 PR 平均审查时长从 X 降至 Y"）——DeepSeek 类 JD 已把这类经历写成硬性加分。

## 四、三种身份的差异化写法

**应届生**：实习前置（头部团队实习是最强信号）；没有实习就把开源/课程项目做成"准实习"（有数字、有 repo 链接）；竞赛写名次+百分位；教育背景可前置。忌：罗列课程成绩、写"精通"清单、项目全是跟教程做的复现（复现也要写出自己的改动与数字）。
**转行者**：第一屏放"桥梁段"——现有背景与目标方向的交集（Java 大数据转数据工程：Spark/Flink 经验直接前置；后端 C++ 转推理：系统功底+已完成的 CUDA/量化学习项目）。转行简历最大的败笔是按原岗位逻辑组织——**用目标方向的词重组你的经历**。补一个 2-4 周能出数字的桥梁项目（见第六节）。
**社招 3 年+**：量化战绩是全部——每个项目必须有规模词（多少卡/多少 TB/多少 QPS/多少 token）和结果词（MFU 从 X 到 Y、利用率从 X 到 Y、成本降 X%）；管理/协作经历压缩，技术深度前置。

## 五、常见致命伤（诊断时逐条检查）

1. 没有数字——二面活不过三问的铁律；
2. 形容词堆砌（"深入理解/精通/熟练掌握"连续出现而无证据）；
3. 技能词与项目脱节（技能栏写了 vLLM，项目里找不到 vLLM 的使用痕迹）；
4. 用自己的行话不用 JD 的行话（初筛关键词匹配直接挂）；
5. 夸大深度标尺（写"改过源码"讲不出改动点）；
6. 与方向无关的经历喧宾夺主（转行者最常见：原岗位内容占 70%）；
7. GitHub 链接是空的或只有 fork——放链接前确保 repo 有 README 和可运行说明。

## 六、2-4 周桥梁项目库（简历缺数字时的补救）

| 方向 | 可出数字的项目 | 能写的量化点 |
|---|---|---|
| 推理 | 在 2 张卡上部署 7B/14B 模型，做量化+批处理调优对比 | TTFT/吞吐/显存的前后对比；GPTQ vs AWQ 精度损失 |
| 训练 | 用 Megatron/DeepSpeed 训一个小模型，扫并行配置 | 不同 TP/PP 配置的吞吐与显存曲线；MFU 计算 |
| 调度 | 用 Kind/minikube 搭 GPU 调度实验（HAMi 共享 vs 独占） | 利用率对比；gang scheduling 前后任务等待时间 |
| 数据 | 拿 FineWeb/Edu 类公开数据做清洗-去重-配比小管线 | 去重率/丢弃率；小模型 proxy 评测前后分 |
| 多模态 | 构造一个万级图文数据集（爬取+清洗+标注抽检） | 规模/一致性 Kappa/对微调效果的提升 |
| 可观测 | 给一个 LLM demo 应用接 OTel，做 token 成本看板 | trace 覆盖率；成本归因到接口的明细 |

补救项目要如实标注"个人项目"——面试官不歧视个人项目，歧视没有数字和思考的项目。

## 七、投递组合建议（收尾时给）

按 requirements.md 的门槛与冷热，给三档：冲刺（大厂核心岗/明星创业公司）、匹配（中厂/云厂商产品线）、保底（数据公司/外包转正路径/实习切入）。转行者建议"保底实习→3 个月转正"与"直接社招"双线并行。
