# 阿里通义（Qwen / Token Foundry / 千问）求职指南

## 公司招聘画像（截至 2026-10-06）

- **组织与渠道**（2026 年重大变化）：**careers-tongyi.alibaba.com 官网已更名"Token Foundry 招聘官网"**——通义实验室招聘体系随 2026-06 成立的 Token Foundry 事业部升级（集团 CEO 直接挂帅"加速大模型冲刺 SOTA"）；另有**千问事业部**（通义应用+夸克+天猫精灵合并，独立招聘站 talent.quark.cn）；校招走 campus-talent.alibaba.com（Token Foundry 与阿里云、千问办公并列独立招聘主体）。注：Qwen 技术负责人林俊旸 2026-03 离职；"Qwen4 训练中"未见官方 JD 表述。
- **节奏与规模**：2026 届秋招超 7000 offer、AI 岗超六成（阿里云/国际/钉钉达 80%）；2027 届实习（2026-03 启动）超八成岗位聚焦 AI；2027 届校招（2026-08 启动）AI 岗占 80%。
- **门槛设计**（五家里最规范）：研究岗"全球 Top 高校博士/硕士优先"，但明确**三条替代路径：顶会一作 或 开源核心代码贡献 或 ASC/SC 竞赛**（阿里星/A Star 通道）；平台岗务实（硕士+3 年+Java/Python 高并发）。
- **薪资**：平台技术专家 30-60K·16；百炼 Agent 算法专家 40-70K·16（猎聘）；社招含阿里系期权体系。

## 在招岗位清单（精选）

### Token Foundry（通义实验室）
| 岗位 | 方向 | 关键要求 |
|---|---|---|
| 代码大模型算法工程师（Qwen-Coder） | 后训练/数据 | 全球 Top 高校博硕优先，**顶会一作或开源/竞赛成果**；RL+代码推理、Coding Agent、Computer-Use/GUI Agent、可验证环境构建 |
| 视觉多模态算法工程师（Qwen-VL/Omni） | 多模态 | 顶尖高校博硕优先；8B~235B MoE 多模态基座、Thinking RL、OCR-free、Grounding |
| Qwen 训练 Infra 前沿技术研究（阿里星，2027 届） | 训练 Infra | **OSDI/SOSP/ASPLOS/MLSys 一作 或 PyTorch/Megatron/DeepSpeed/vLLM/TensorRT-LLM 核心贡献 或 ASC/SC 竞赛**；C++/Python、CUDA/Triton |
| 基础平台研发工程师 | 推理框架/微调/MaaS | 硕士+，ACM 或 HuggingFace/ModelScope 经验优先 |
| post-training 算法工程师 / LLM Research / 大模型智能体研究 | 对齐/研究/Agent | 官网序列岗 |
| 通义万相算法工程师（Wan） | 视频/图像生成 | 校社实习，杭/京 |

### 2026/2027 校招"七类新设 AI 岗"
AI 应用研发 / AI 应用算法 / **AI Agent 优化工程师** / **Agent Infra 工程师** / AI 数据工程师 / AI Infra 工程师 / AI SRE（另首次出现 AI 全栈工程师）。

### 社招：阿里云 PAI / 百炼
- **AI 推理平台-百炼技术专家**（含金量最高的社招 JD 之一）：团队负责百炼/千问 AI 平台/Qwen Cloud 三线，万级 QPS 弹性推理；技术点 **PTU 推理工具链、多 LoRA（Megatron+DeepSpeed 训推一体）、Agent Studio Loop、OpenTelemetry 观测、Token 计费**；硕士+3 年 Java/Python 高并发。
- 百炼 Agent 高级算法专家：40-70K·16，5-10 年。

## 技术底色（面试准备）

- Qwen Team 算法分 **LLM / Vision-Language / Audio-Language 三大板块**；post-training 细分通用/安全/Agent。
- 平台岗 JD 枚举的技术栈就是考纲：推理服务设计（万级 QPS）、多 LoRA 训推一体、OTel 观测——系统设计按"模型服务平台"准备（调度/弹性/计费/观测四层）。
- 研究岗面试核**可核查证据**：论文链接、PR 记录、竞赛名次——简历上写到可点击核验的粒度。

## 独特关键词

Token Foundry、千问事业部/千问办公、Qwen Cloud、百炼（Model Studio）、DashScope、PAI、魔搭 ModelScope、通义万相 Wan、Qwen-Agent、PTU、TPM 预留、多 LoRA、Agent Studio Loop、Token Plan、阿里星/A Star Program、T-Star Lab、"开源社区维护投入"（JD 明写，字节/腾讯少见）。

## 投递建议

- **应届**：HC 体量五家最大（7000+ offer、AI 岗 80%），校招是主通道；工程背景投"七类新设 AI 岗"（Agent Infra/AI SRE 是新口）；研究背景冲通义实验室（三条替代路径挑一条把证据做实）。
- **社招平台/后端**：百炼技术专家 JD 是标杆——Java 高并发+分布式功底+懂推理服务，是后端转 AI 平台的最佳落点。
- **开源贡献者**：JD 明写"开源社区维护投入"，vLLM/Megatron/ModelScope 的 PR 在这里是硬通货。
- **多模态方向**：Qwen-VL/Omni 团队持续招，生态最大（6 亿次下载/17 万衍生模型）意味着经验可迁移性最好。

*来源：careers-tongyi.alibaba.com（4 份 JD 实抓）、campus-talent.alibaba.com、careers.aliyun.com（百炼 JD 实抓）、talent.quark.cn、财联社/新浪（校招数据）、Qwen 知乎招聘帖、猎聘。*
