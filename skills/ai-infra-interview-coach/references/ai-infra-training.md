# AI Infra · 训练方向（分布式训练/Megatron/RL Infra）面经库

## 岗位画像
- 干什么：千亿/万亿参数模型高效稳定训练；RL Infra 是 2026 新热点（腾讯专设方向）。
- 门槛：本科可投硕士主流，算子方向近乎硕博+HPC；C+++Python+Linux 是最大公约数。
- 必备：PyTorch 深入（dispatcher/自动求导/显存管理）；DP/TP/PP/EP 原理与配比；Megatron-LM/DeepSpeed/FSDP **至少一套"改过源码"级经验**（美团 JD 原话："用过或改过，不只是跑过 demo"）；BF16/FP8；checkpoint 容错。
- 加分：NCCL/RDMA/HCCL 底层、FlashAttention/Ring Attention/MoE 专家并行、万卡实战、昇腾适配（部分线已转硬性）。
- 在招：字节 AML/Seed、阿里 PAI、腾讯机智/混元、华为昇腾生态、DeepSeek（~150 HC）、小米 MiMo、美团北斗、小红书、九坤/幻方。

## 面试流程（3-4 轮）
一面八股+手撕 → 二面系统设计+源码深挖 → 三面项目/主管面；社招加交叉面。

## 真题库

### 八股
1. ZeRO-1/2/3 分别切了什么（优化器状态/梯度/参数）？（腾讯/百度/MiniMax）
2. **ZeRO-3 通信量是 ZeRO-1/2 的多少倍？——答 1.5 倍**（同上，高频数字题）
3. 训练 70B 模型需要多少显存？（多公司必考）
4. BF16 vs FP16 区别与精度控制（美团）
5. NCCL vs Horovod；PyTorch DDP 原理；RDMA 在多节点训练的作用（通义；腾讯混元实习直接考 RDMA）
6. TP+PP+DP 3D 并行通信开销计算与配比（美团北斗/MiniMax/阶跃）
7. MoE 专家负载不均衡怎么解？All-to-All 通信如何优化？（同上）
8. 给定 tokens 数估算训练时间（牛客）
9. loss spike / 梯度震荡怎么修？（跨公司高频）

### 手撕
1. CUDA shared memory 优化的矩阵乘法：写 kernel+block/grid 设计思路，不要求可运行（通义）
2. GEMM tiling/Tensor Core 实现+**Roofline 分析 compute/memory-bound**（美团）
3. **Ring AllReduce 手撕+推导**：reduce-scatter+all-gather 两阶段；单卡通信量 2(N-1)·M/N≈2M 与卡数无关；Ring vs Tree 适用（多公司）
4. MLP 前向/反向+SGD（通义）；MoE 路由 Top-K+auxiliary loss（美团/智谱）

### 系统设计（社招占比最高）
1. 万卡级分布式训练系统，通信瓶颈怎么处理（通义千问）
2. 100B+ 参数/2000+ GPU 训练系统含 OOM 恢复；追问 fat-tree vs dragonfly（OpenAI 方向）
3. 万卡中断快速恢复——checkpoint 三策略：Sharded/Async/Selective（2026 高频）
4. Llama 低 MFU/OOM/hang 诊断流程：Nsight/PyTorch Profiler/NCCL 日志（Meta 方向）

### 项目深挖
1. "MFU 从 X% 提到 Y% 怎么做的"——量化成果必问
2. 训练崩溃/OOM 怎么解决、个人最大贡献点（通义）

## 重点题答题要点

**显存计算模板**：混合精度+Adam ≈ **2×参数量**（FP16 权重+梯度）+**12×参数量**（FP32 主权重+动量+方差）+ activations。70B→约 980GB+ 仅权重与优化器 → 顺势引出 ZeRO→3D 并行。这是"为什么必须切"的标准开场。

**ZeRO 通信量**：ZeRO-1/2≈基线 1×；ZeRO-3 前反向各多一次 all-gather → 1.5×。

**Ring AllReduce 推导**：两阶段合计每卡收发 2(N-1)·M/N≈2M 与 N 无关；带宽最优、延迟随 N 线性 → 大消息 Ring、小消息/浅集群 Tree。

**loss spike 诊断**（忌答"直接降 lr"）：先分类——坏数据样本/lr 过高/数值精度（fp16 溢出）哪一类，再对症（数据过滤/warmup 调整/bf16 切换），讲第一性原理。

## 挂人点
① 说"用过 Megatron"但没改过源码——追问 parallel config 立刻露馅；② 手撕 kernel 不写边界检查与 bank conflict 分析；③ loss spike 只会降 lr；④ 系统设计没有弹性与容错维度（万卡周均故障是常态）。
