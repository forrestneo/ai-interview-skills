# AI Infra · 推理方向（vLLM/量化/投机解码）面经库——当前最热

## 岗位画像
- 干什么：让模型推得便宜、快、稳。
- 门槛：与训练向类似，但**vLLM 源码级理解是分水岭**；社招 3 年+LLM 推理或 GPU 高性能经验常见（猎聘口径）。
- 必备：vLLM/SGLang/TensorRT-LLM 源码级（Scheduler、PagedAttention block 映射）；KV cache 管理（显存估算/prefix 共享）；Continuous Batching；量化落地（GPTQ/AWQ/INT8/FP8）。
- 加分：CUDA/Triton 手写 kernel、PD 分离、投机解码（EAGLE/Medusa）、CUTLASS。
- 纠偏：约半数 AI Infra 岗不需要 CUDA，但推理工程师象限里 CUDA 是强加分。

## 面试流程（3-5 轮）
一面：推理八股+手撕（字节要求 bug-free）；二面：源码深挖；三面：推理服务系统设计；提前批有笔试（美团：C++ 读程序+LCA Hard）。

## 真题库

### 八股
1. **为什么推理要 KV Cache？decode 阶段为什么只缓存 KV 不缓存 Q？**（阿里原题）
2. PagedAttention 如何避免 KV cache 碎片？Block 映射怎么实现？copy-on-write 与 prefix sharing（beam search 场景）（字节；快手考"为什么需要动态管理 KV cache 显存"）
3. vLLM Scheduler 源码：请求如何进队列、调度算法是什么（源码高频）
4. Attention 怎么算？为什么除以 √d？（字节大模型算法岗-04）
5. FlashAttention v2 比 v1 改进；**为什么没减少计算量却能加速**（IO-aware）；causal mask 整块跳过；backward 重算 P（字节/美团）
6. GPTQ 流程（Hessian 逐列最小化误差）；AWQ 的 activation smoothing；PTQ vs QAT；SmoothQuant vs FP8 场景（美团/Meta/字节）
7. **投机解码原理（小模型猜+大模型批量验证）；高 batch 下为何优势消失**（拼多多提前批）
8. MLA vs MHA：latent 压缩如何让 KV cache 减少 5-10 倍；GQA/MQA 优势；GLM-4 为何选 GQA（Kimi/智谱/美团）；Lightning Attention 线性复杂度（快手）
9. Prefill vs Decode 特性差异与各自优化；two-batch overlap（牛客）

### 手撕
1. **online softmax CUDA kernel：warp reduce 求 max/sum+bank conflict 分析**（字节/智谱/美团；53AI 题库方向）
2. 手撕 MultiHeadAttention（含 QKV）——字节真题（"90% 会考"）
3. 变长序列 attention、高效 GEMM 分块（MiniMax/阶跃）
4. Top-k sampling、Beam Search、BPE tokenizer（字节/智谱/美团）
5. 算法题：前缀和取模+哈希（拼多多）；字符串区间反转多次查询、螺旋矩阵（小红书）

### 系统设计
1. **10 万（乃至百万）QPS 的 LLM 推理服务**：异构调度、动态批、成本优化（美团/2026 画像）
2. **KV cache 成本 10 倍高于预期，如何诊断修复——陷阱题：不能答"加内存"**。正确思路分层：批调度策略→prefix 命中率→量化→缓存逐层排查（OpenAI 方向）
3. 长上下文（1M+）：PagedAttention+Radix Tree+FlashDecoding（智谱）
4. GPU 有限时推理与微调共存：资源分配、时延吞吐权衡（场景题）

### 项目深挖
1. 推理优化项目的 TTFT/吞吐收益怎么测的？流量模型是什么？（vLLM/自研引擎项目必问）

## 重点题答题要点

**KV cache 显存公式（必考）**：`2 × 层数 × kv_head 数 × head_dim × 序列长 × batch × 精度字节`。先公式再代数（Llama-7B/33 层/GQA 例），顺势引出 PagedAttention（block+block table 治理内部/外部碎片）→ prefix sharing → PD 分离（prefill 计算密集/decode 访存密集）。

**为什么只缓存 KV 不缓存 Q**：decode 每步只算当前 token 的 Q，历史 Q 不再参与后续 attention；K/V 每步都要被复用。

**投机解码高 batch 失效**：大模型验证时算力已饱和，"顺带验证"收益消失；且接受率随 batch 下降。

**online softmax**：两次遍历合并——维护 running max 与 rescale 的 running sum（数值稳定且单遍读取）；CUDA 版 warp shuffle reduce（`__shfl_down_sync`）做块内归约；shared memory 布局用 padding/swizzle 避 bank conflict。

**FlashAttention 加速本质**：计算量不变，靠 tiling 让 SRAM 内完成 attention、HBM 读写 O(N²)→O(N²·d/M)大幅减少——IO-aware 是关键词。

## 挂人点
① 背了 PagedAttention 名词画不出 block table；② 量化只会"INT8 更快"，讲不出误差补偿；③ 服务扛不住答"加机器"——没有 batching/缓存/量化/PD 分层思维；④ 手撕不写 `__syncthreads()` 或忽视 safe softmax。
