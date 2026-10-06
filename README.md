# 大模型面试 · AI 基础设施岗位面试教练（ZCode Skill）

[![skill](https://img.shields.io/badge/skill-llm--interview-blue)]() [![directions](https://img.shields.io/badge/岗位方向-7-green)]() [![companies](https://img.shields.io/badge/焦点公司-5-orange)]() [![questions](https://img.shields.io/badge/面经真题-150%2B-red)]() [![license](https://img.shields.io/badge/license-MIT-lightgrey)]()

> 一个装进 ZCode 的**大模型/AI 基础设施岗位面试教练**：双维度知识库——按岗位方向（7 大领域面经）× 按公司（5 家头部模型公司档案），内置模拟面试、简历优化、备考计划、公司选择六种工作流。150+ 道带公司出处的真题、答题要点与挂人点。

**AI Infra 训推/调度 · Data Infra · 大模型数据 · 多模态 · AI 可观测 × DeepSeek · Kimi · MiniMax · 智谱 · 通义**

---

## 这是什么

一个 [ZCode 技能](https://docs.zcode.dev)（也可用于任何支持 SKILL.md 规范的 agent 环境），把"AI 基础设施类技术岗怎么面"做成可复用的教练。知识库按两个维度组织，一次求职通常两维配合：

```
按岗位方向（练技术面）                按公司（选公司、对偏好）
├─ AI Infra-训练（ZeRO/3D并行）       ├─ DeepSeek（年轻+竞赛，9月150HC纯工程）
├─ AI Infra-推理（PagedAttention）    ├─ Kimi（K3三件套，穿越计划实习期权）
├─ AI Infra-容器调度（K8s/GPU）       ├─ MiniMax（不看资历，Lightning Attention）
├─ Data Infra（LSM/ClickHouse/HNSW）  ├─ 智谱（算法岗必问数据构建）
├─ 大模型数据链路（MinHash/配比/DPO）  └─ 通义（Token Foundry，三条替代路径）
├─ 多模态数据算法（CLIP/DDPM）
└─ AI 可观测（SLO/OTel/LLM四指标）
```

## 六种工作流

| 模式 | 触发说法 | 产出 |
|---|---|---|
| **A 模拟面试** | "面我""模拟一面" | 按真实轮次出题→三档判卷（✅⚠️❌）→✅的题追问一层→终面报告 |
| **B 备考计划** | "还有一个月怎么准备" | 周计划（手撕五件套+八股三件套+项目闭环+投递节奏） |
| **C 项目打磨** | 贴简历项目 | 量化四问，答不出①标"高危"并给补数字做法 |
| **D 速查答疑** | "XX 岗考什么" | 题库概览/真题+要点+出处 |
| **E 简历优化** | "帮我改简历" | JD 关键词覆盖表+四级深度标尺校准+before/after 重写+投递三档 |
| **F 公司选择** | "DeepSeek 还是智谱" | 偏好×背景匹配矩阵+岗位逐岗判定+offer 三栏对比 |

核心纪律：先定位再服务；**多数人死于追问而非首问**（✅的题也要追问）；**没有量化数字的项目在二面活不过三问**；库外题标"推演题"不装真题；公司偏好差异必须体现（不给通用建议）。

## 安装

```bash
git clone https://github.com/<你的用户名>/ai-interview-skills.git

# 全局可用（推荐）
cp -r ai-interview-skills/skills/llm-interview ~/.zcode/skills/

# 或仅项目内可用
cp -r ai-interview-skills/skills/llm-interview <你的项目>/.zcode/skills/
```

安装后按描述自动触发，也可 `/skill llm-interview` 强制加载。

## 使用示例

新开一个 ZCode 对话，直接说话即可：

```text
> 我想面大模型推理岗，还有一个月，模拟面试一面          # → 模式 A
> 我是 Java 后端 3 年，帮我把简历改成能投数据工程岗的   # → 模式 E
> 我想面 DeepSeek，应届硕士有 ACM 银牌，能投什么岗？    # → 模式 F
> MiniMax 和智谱怎么选？我 32 岁，后端转的             # → 模式 F

# 判卷输出格式
【判定】✅通过 / ⚠️勉强 / ❌挂
   → 【缺了什么】… → 【标准要点】… → 【追问】…
```

## 项目结构

```
ai-interview-skills/
├── README.md
├── LICENSE
└── skills/
    └── llm-interview/                      # 大模型面试（唯一技能）
        ├── SKILL.md                        # 工作流：定位→双维度路由→六种模式
        └── references/                     # 15 份知识文件（渐进披露）
            ├── requirements.md             # 岗位对比/门槛/转型路径总表
            ├── resume-guide.md             # 简历方法论：公式/四级标尺/关键词库/桥梁项目
            │── ── 方向面经（7 份）──
            ├── ai-infra-training.md        # 训练：ZeRO通信量/Ring AllReduce推导/万卡设计
            ├── ai-infra-inference.md       # 推理：KV cache公式/投机解码/CUDA手撕
            ├── ai-infra-platform.md        # 调度：GPU平台三问框架/gang scheduling
            ├── data-infra.md               # 数据：ClickHouse四层/LSM三件套/HNSW陷阱
            ├── llm-data.md                 # 数据链路：MinHash+LSH/配比/LoRA参数/DPO推导
            ├── multimodal.md               # 多模态：CLIP InfoNCE/DDPM推导/图文去重
            ├── ai-observability.md         # 可观测：监控四层模板/SLO告警/LLM四指标
            │── ── 公司档案（6 份）──
            ├── comparison.md               # 五家对比矩阵/偏好匹配/投递组合模板
            ├── deepseek.md / kimi.md / minimax.md / zhipu.md / tongyi.md
```

每份面经统一五段式：**岗位画像 → 面试流程 → 真题库（八股/手撕/系统设计/项目深挖，带公司+轮次）→ 重点题答题要点（含公式模板）→ 挂人点**。

## 数据来源与时效

- 面经真题：牛客/知乎/CSDN/博客园真实面经（AIInfraGuide 65+ 公司 181+ 场、博客园 13 家分司真题、小林 note、llm-study 100 题、牛客 ClickHouse 170 题等）；面经是候选人回忆，题面会有偏差，出处能标的都已标。
- 公司数据：官网招聘页 + Boss直聘/牛客/脉脉/媒体报道交叉，**截至 2026-10-06**；模型公司招聘变化极快，投递前请上官网核对。
- 薪资：全部为二手样本（挂价/媒体口径），已逐条标注来源。

## 已知局限

- 中国招聘市场视角（海外仅作对照）；真题以大陆公司为主。
- 五家焦点公司之外（字节 Seed、腾讯混元、阶跃等）按通用框架推演并明确标注，不伪装库内数据。
- 可观测方向带出处的原题样本较少；调研底稿（约 130 次检索的完整来源 URL）不在本仓库。

## Roadmap

- [ ] 补充字节 Seed / 腾讯混元公司文件
- [ ] 具身智能数据方向独立成篇
- [ ] 手撕题参考实现（assets/ 下可运行的 CUDA/PyTorch 参考代码）
- [ ] 题库英文版（海外投递）

## 贡献

欢迎补充面经（请附公司+轮次+尽量原题）、纠正过时数据。方向类新文件请遵循五段式结构；公司类新文件请对照 deepseek.md 的格式。

## License

[MIT](LICENSE)
