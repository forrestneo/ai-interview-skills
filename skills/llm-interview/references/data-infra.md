# Data Infra（数据库内核/OLAP · 湖仓平台 · 向量库/RAG）面经库

## 岗位画像
- 三个子层（门槛与薪资递减）：**内核/OLAP**（C++/Rust+查询优化+向量化+存储引擎，门槛最高）→ **流处理**（Flink+Kafka+Java）→ **平台/湖仓**（Java/Go+Spark+Iceberg，岗位最多、后端可转）。
- 新增方向：向量库（Zilliz/腾讯）与 RAG 管道——AI 经验正从加分项变标配（腾讯 JD 明写"LLM/Agent（MCP、RAG）开发经验"加分；美团职位标题直接叫"AI+数据"）。
- 入场券：CMU 15-445 → MiniOB/OceanBase 训练营 → **给开源数据库提 PR**（智联内核岗把"ClickHouse GitHub 提交记录"写进硬性要求）。
- 在招：Zilliz（内核 40-50K·16）、镜舟 StarRocks、SelectDB（Doris）、字节 ByteHouse、阿里云大数据、美团、小红书。

## 面试流程
内核岗：C++/数据结构+OS → 内核八股（B+树/LSM/MVCC）+15-445 lab 逐个追问 → 系统设计。平台岗：Java/Go+Flink/Spark 八股+数仓场景题。

## 真题库

### 内核/OLAP 八股
1. **MySQL 为什么用 B+树不用 B 树/哈希？**——树高/范围查询/缓存友好三点（阿里一面 27 问；微众银行）
2. 聚簇 vs 非聚簇索引、索引失效场景（微众 2025）
3. **LSM Tree：为什么牺牲读换取写？WAL→MemTable→SSTable 全流程；Bloom Filter 如何缓解读放大；Leveled vs Tiered Compaction 取舍**（阿里/网易/百度/美团 180 题汇总）
4. MVCC：版本链、ReadView 判定规则、快照读 vs 当前读（掘金 InnoDB 高频）
5. **ClickHouse 为什么快（必考）**：列存+压缩、向量化执行+SIMD、MergeTree 稀疏索引、多核并行——追问短板"缺 CBO"（牛客 170 题；字节 data）
6. MergeTree 源码级：granule 划分、primary.idx 稀疏索引、.mrk 标记与 .bin 映射（博客园源码分析）
7. Doris/StarRocks：FE/BE 架构、三种数据模型、向量化、CBO、与 CH 对比（CSDN 精选）
8. 查询优化器：启发式 vs CBO、join 顺序枚举（CMU 15-445 Lecture 12-14）

### 湖仓/平台八股
1. Flink：**Watermark 处理乱序机制、Event vs Processing Time、Checkpoint 两阶段提交全流程**、反压定位、CEP（拼多多/小红书/阅文）
2. Spark：SortShuffle 原理、**数据倾斜八连问**（加盐/两阶段聚合）、调优参数（字节 2026 题库）
3. Kafka：为什么快（顺序写/零拷贝/批量）；消息不丢不重（acks/幂等/事务）；ISR；Rebalance（京东/网易/知乎）
4. Iceberg：表格式 vs Hive 表、隐藏分区、snapshot 时间旅行、ACID、与 Hudi/Delta 对比（CSDN 精选）
5. 数仓：分层理由、拉链表、缓慢变化维、窗口函数手写（数仓 100 题）

### 向量库/RAG
1. **为什么需要 ANN？HNSW/IVF/PQ 三者怎么区分**——HNSW 分层图参数 M/efConstruction/efSearch 对召回与速度影响；IVF 聚类分桶+nprobe；PQ 压缩损失（llm-study 100 题；美团考 Milvus 索引选择）
2. **HNSW 内存陷阱**：100 万条 128 维要同时存图结构+原始向量（Milvus 官方，常问坑点）
3. metadata filter 放检索前还是后？reranker 为什么比纯向量召回好？
4. 系统设计：**企业级 RAG 知识库**——多格式解析、增量更新不重建索引、权限隔离、千万级文档性能（牛客场景复盘）

### 手撕
1. CMU 15-445 BusTub 四 lab（Buffer Pool→B+Tree→并发→查询执行）逐个追问：LRU-K、脏页落盘、latch crabbing——内核岗简历核心项目
2. 手写余弦相似度/topK 检索；MinHash 签名计算

## 重点题答题要点

**ClickHouse 为什么快**（四层展开）：① 列存+按列压缩（同类型数据压缩比高、扫描列少）；② 向量化执行引擎+SIMD；③ MergeTree 稀疏索引（每 granule 一个 mark，主键索引常驻内存，级联 minmax 跳数）；④ 单机多核并行+分区裁剪。短板主动说：没有成熟 CBO、join 能力弱、更新是异步 mutation——主动讲短板是加分动作。

**LSM 三件套**：写路径 WAL 保崩溃一致 → MemTable 内存有序结构 → flush 成 SSTable 不可变文件；读路径 memtable→新到旧 SSTable+每个 SSTable 一个 Bloom filter 拦截空查；Compaction：Leveled（空间/读放大小、写放大大）vs Tiered（反之）——按业务读写比选择。

**Exactly-Once 端到端加分答法**：source 可重放（Kafka offset）+Flink Checkpoint 两阶段提交+sink 幂等/事务——三段缺一不可。

## 挂人点
① "ClickHouse 快"只背四点但说不出稀疏索引为什么省内存（granule+mark 机制）；② Flink 只会用 API 讲不清 Checkpoint barrier 流转；③ 向量库只知道"存 embedding"，讲不清 HNSW 参数与内存代价；④ 没有 15-445 lab 或等价项目时被逐层追问没有退路。
