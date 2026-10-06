# AI Infra · 容器/调度方向（K8s/GPU 平台）面经库

## 岗位画像
- 干什么：GPU 集群的调度、配额、共享、利用率——AI 平台的地基。
- **五类岗位中对后端/运维/SRE 背景最友好的一条路**：K8s+Go 功底可 6-12 个月切入。
- 必备：Kubernetes 深入（调度器框架/设备插件/Operator）+ Go + Python/C++ 至少一门；GPU 资源管理与共享调度。
- 加分：Volcano/Kueue/Kubeflow/YuniKorn/Karmada、HAMi 等 GPU 虚拟化（MIG/显存切分）、Ray/Slurm、Linux 内核（调度器/cgroups）。
- 在招：小红书（GPU 调度 30-60K·16）、腾讯 TIONE、B 站、九坤等量化私募平台岗。

## 面试流程
与 SRE/平台岗接近：一轮 K8s 八股+场景排障 → 二轮平台系统设计（GPU 调度/配额/超卖）→ 三轮项目。LeetCode 中等+K8s 源码级追问。

## 真题库

### 八股
1. **GPU 如何通过 device plugin 上报资源？`nvidia.com/gpu` extended resource 的调度流程**（GPU 平台岗 30+ 考点）
2. 拓扑感知调度：GPU 亲和性、NUMA、NVLink 拓扑（同上）
3. **GPU 共享方案对比：vGPU/分时/HAMi/MIG——多租户推理为什么选 MIG**（物理隔离、故障域、QoS 确定性）
4. Pod 一直 Pending / CrashLoopBackOff 怎么排查？（SRE 100 题高频）
5. Service 类型、Ingress 原理、Init 容器 vs Sidecar（同上）
6. **Volcano 的 Gang Scheduler 为什么对分布式训练是必需的**——训练任务作为原子单元整进整出，避免部分调度导致死锁与抢占浪费（AI 平台岗知识考点）

### 系统设计（本岗重心）
1. **设计 K8s 之上的 GPU 训练平台：配额管理（静态隔离 vs 全局弹性共享）、算力超卖、利用率从 ~30% 提到 70%+**（博客园/火山引擎真题方向）
2. 竖井隔离 vs 共享池模式：隔离性、计费计量、抢占
3. 训练平台的 checkpoint/故障恢复与弹性分布式训练设计（知乎 305 题版）
4. 云原生 AI 服务弹性调度方案（通义）
5. 设计 GPU 调度系统（OpenAI 方向）

### 项目深挖（追问链）
1. 集群利用率怎么统计？（分卡级/pod 级/SM 利用率，区分占用率与真实利用率）
2. 超卖后怎么保证高优任务 SLO？（优先级队列+degrade 预算+MIG 物理隔离）
3. MIG 切分粒度怎么定？

## 重点题答题要点

**GPU 平台设计三问框架**（系统设计万能模板）：
- **怎么测**：利用率分层统计（GPU util vs SM 活动率 vs 显存占用），多租户按 namespace/pod 归因；
- **怎么提**：gang scheduling 消除排队碎片 → quota 弹性借还 → 超卖+优先级抢占 → checkpoint 容器迁移；
- **怎么不劣化 SLO**：高优队列、degrade 预算、MIG 物理隔离、告警熔断。

**device plugin 流程**：DaemonSet 里 vendor plugin 通过 gRPC RegisterDevicePlugin 向 kubelet 注册 → ListAndWatch 上报 device ID → Pod 申请 `nvidia.com/gpu` → kubelet 分配并传 env（NVIDIA_VISIBLE_DEVICES）→ 容器运行时挂 GPU。追问点：为什么是 extended resource 而不是原生整数量（不进 scheduler 的真实占用视图→催生 GPU 共享方案）。

## 挂人点
① 只部署过 K8s 不懂调度器扩展点（scheduler framework 的 plugin 位置）；② 超卖答成"无脑加副本"；③ 没摸过 GPU（nvidia-smi 的 util/memory 两列差异都说不清）；④ 讲 gang scheduling 只说概念说不出"为什么不用默认调度器"的死锁场景。
