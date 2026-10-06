# AI 技术岗面试教练 · ZCode Skills

[![skills](https://img.shields.io/badge/skills-2-blue)]() [![coverage](https://img.shields.io/badge/岗位方向-7-green)]() [![companies](https://img.shields.io/badge/焦点公司-5-orange)]() [![questions](https://img.shields.io/badge/面经真题-150%2B-red)]() [![license](https://img.shields.io/badge/license-MIT-lightgrey)]()

> 一套装进 ZCode 的 AI 基础设施岗位面试知识库与教练：**150+ 道带公司出处的真题、答题要点与挂人点**，覆盖七大技术方向 + 五家头部大模型公司；内置模拟面试、简历优化、备考计划三种工作流。

**AI Infra · Data Infra · 大模型数据 · 多模态 · AI 可观测 × DeepSeek · Kimi · MiniMax · 智谱 · 通义**

---

## 这是什么

两个互补的 [ZCode 技能](https://docs.zcode.dev)（也可用于任何支持 SKILL.md 规范的 agent 环境），把"AI 基础设施类技术岗怎么面"这件事做成了可复用的教练：

| 技能 | 组织维度 | 干什么 |
|---|---|---|
| **ai-infra-interview-coach** | 按**岗位方向**（7 个） | 面经真题库 + 模拟面试 + 备考计划 + 简历优化 + 项目闭环打磨 |
| **llm-interview** | 按**公司**（5 家） | 公司选择咨询 + 岗位匹配 + 按公司特色备考 + 投递策略 |

实际求职时两个配合：先用 `llm-interview` 定"投哪家哪个岗、按什么偏好包装"，再用 `ai-infra-interview-coach` 练技术面。

## 覆盖范围

**七大岗位方向**（ai-infra-interview-coach）：

```
AI Infra-训练（ZeRO/3D 并行/Ring AllReduce/万卡系统设计）
AI Infra-推理（PagedAttention/量化/投机解码/CUDA 手撕）
AI Infra-容器调度（K8s/GPU 调度/gang scheduling/平台设计三问）
Data Infra（LSM/ClickHouse/MergeTree 源码/HNSW/企业级 RAG 设计）
大模型数据链路（MinHash+LSH/数据配比/LoRA 参数/DPO 推导）
多模态数据算法（CLIP InfoNCE/DDPM 推导/图文去重/标注一致性）
AI 可观测（三支柱/SLO 告警/采样策略/LLM 四指标）
```

**五家焦点公司**（llm-interview）：DeepSeek、月之暗面 Kimi、MiniMax、智谱 GLM、阿里通义（Qwen/Token Foundry）——在招岗位清单、招聘偏好（如 DeepSeek 偏年轻+竞赛、MiniMax"不看资历只看能力"）、薪资口径、独特 JD 关键词、面试特色（如 MiniMax 不考八股考 Lightning Attention）。

**每份面经包含**：面试流程（几轮考什么）→ 四类真题（八股/手撕/系统设计/项目深挖，**带公司+轮次出处**）→ 重点题答题要点（含公式模板）→ 挂人点。

## 安装

```bash
# 方式一：整体 clone 到用户技能目录（全局可用）
git clone https://github.com/<你的用户名>/ai-interview-skills.git
cp -r ai-interview-skills/skills/* ~/.zcode/skills/

# 方式二：只要其中一个技能
cp -r ai-interview-skills/skills/ai-infra-interview-coach ~/.zcode/skills/
cp -r ai-interview-skills/skills/llm-interview ~/.zcode/skills/

# 方式三：仅项目内可用（放到项目根的 .zcode/skills/ 或 .agents/skills/）
cp -r ai-interview-skills/skills/* <你的项目>/.zcode/skills/
```

安装后无需配置——技能按描述自动触发，也可以用 `/skill <技能名>` 强制加载。

## 使用示例

新开一个 ZCode 对话，直接说话即可触发：

```text
# 触发模拟面试（ai-infra-interview-coach）
> 我想面大模型推理岗，还有一个月，模拟面试一面
# 触发简历优化
> 我是 Java 后端 3 年，帮我把简历改成能投数据工程岗的
# 触发公司咨询（llm-interview）
> 我想面 DeepSeek，应届硕士有 ACM 银牌，能投什么岗？
> MiniMax 和智谱怎么选？我 32 岁，后端转的

# 判卷输出格式
【判定】✅通过 / ⚠️勉强（缺关键点）/ ❌挂（对照挂人点）
   → 【缺了什么】… → 【标准要点】… → 【追问】…
```

内置的工作流纪律：先定位（岗位/身份/背景/时间）再服务；✅ 的题也要追问一层（**多数人死于追问而非首问**）；项目没有量化数字在二面活不过三问；题库外的题标注"推演题"不伪装真题。

## 项目结构

```
ai-interview-skills/
├── README.md
├── LICENSE
└── skills/
    ├── ai-infra-interview-coach/          # 按岗位方向的教练
    │   ├── SKILL.md                       # 工作流：定位→路由→五种模式
    │   └── references/                    # 渐进披露的知识库
    │       ├── requirements.md            # 岗位对比/门槛/转型路径总表
    │       ├── resume-guide.md            # 简历方法论：公式/四级标尺/关键词库/桥梁项目
    │       ├── ai-infra-training.md       # 训练方向面经
    │       ├── ai-infra-inference.md      # 推理方向面经
    │       ├── ai-infra-platform.md       # 容器调度方向面经
    │       ├── data-infra.md              # 数据库内核/湖仓/向量库面经
    │       ├── llm-data.md                # 大模型数据链路面经
    │       ├── multimodal.md              # 多模态数据算法面经
    │       └── ai-observability.md        # AI 可观测/AIOps 面经
    └── llm-interview/                     # 按公司维度的教练
        ├── SKILL.md
        └── references/
            ├── comparison.md              # 五家对比矩阵/偏好匹配/投递组合
            ├── deepseek.md / kimi.md / minimax.md / zhipu.md / tongyi.md
```

## 数据来源与时效

- 面经真题：牛客/知乎/CSDN/博客园真实面经（AIInfraGuide 65+ 公司 181+ 场、博客园 13 家分司真题、小林 note、llm-study 100 题、牛客 ClickHouse 170 题等），出处尽量标注公司+轮次——面经是候选人回忆，题面会有偏差。
- 公司岗位数据：官网招聘页 + Boss直聘/牛客/脉脉/媒体报道交叉，**截至 2026-10-06**；模型公司招聘变化极快，投递前请上官网核对。
- 薪资：全部为二手样本（招聘平台挂价/媒体汇总），已逐条标注来源，实际成交可能不同。
- 调研底稿（约 130 次检索的完整来源 URL）未包含在本仓库中。

## 已知局限

- 中国招聘市场视角（海外仅作对照）；面经以大陆公司为主。
- 五家焦点公司之外（字节 Seed、腾讯混元、阶跃等）技能会按通用框架推演并明确标注，不伪装成库内数据。
- 真题密度在 AI Infra-推理/训练、数据方向最高；可观测方向带出处的原题样本较少。

## Roadmap

- [ ] 补充字节 Seed / 腾讯混元公司文件
- [ ] 具身智能数据方向独立成篇
- [ ] 手撕题参考实现（`assets/` 下可运行的 CUDA/PyTorch 参考代码）
- [ ] 题库英文版（海外投递）

## 贡献

欢迎补充面经（请附公司+轮次+尽量原题）、纠正过时数据、新增方向或公司文件。PR 前请确认新增 reference 遵循现有五段式结构（岗位画像 → 面试流程 → 真题库 → 答题要点 → 挂人点）。

## License

[MIT](LICENSE)
