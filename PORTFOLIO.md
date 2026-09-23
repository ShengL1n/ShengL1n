# Portfolio Architecture & Roadmap

面向「1–2 年内跳中大厂（滴滴/网易+）」的组合仓规划。原则：**业务可讲、可运行、可量化**，禁止精读 clone 当项目。

---

## 1. 分层架构

```text
┌─────────────────────────────────────────────────────────────────┐
│ 业务应用层                                                        │
│   VoltSage(能源运维 Agent)   HarborCheck/DocMill(物流单证)          │
├─────────────────────────────────────────────────────────────────┤
│ 编排 / 工具面                                                      │
│   FlowForge(DAG/补偿)       ToolGate(MCP/Tools 网关)               │
├─────────────────────────────────────────────────────────────────┤
│ 数据 / 检索                                                        │
│   HydroSeek(BM25+向量+RRF)  linflux(有界批处理/对账管道)            │
├─────────────────────────────────────────────────────────────────┤
│ 模型接入 / 质量与成本                                                │
│   PolyRoute(LLM 网关)       RAGLens(RAG 评测)     Lumenscope(成本) │
├─────────────────────────────────────────────────────────────────┤
│ 基础功                                                            │
│   infra-kata (mini-rpc / mini-cache / mini-limiter)               │
└─────────────────────────────────────────────────────────────────┘
```

## 2. 职责与面试定位

| 仓 | 一句话 | 主攻考点 |
|----|--------|----------|
| PolyRoute | 多模型网关 | 路由、配额、成本 |
| RAGLens | RAG 评测平台 | Hit@K / MRR / Judge、bad case |
| Lumenscope | LLM 成本/延迟归因 | span、瀑布、feature 出账 |
| VoltSage | 能源运维 Agent | 可解释诊断 + 工单 |
| HarborCheck | 单证核对 + DocMill | 规则优先、schema 门禁 |
| FlowForge | 可恢复工作流 | DAG、重试、补偿、checkpoint |
| ToolGate | 工具/MCP 网关 | 鉴权、限流、审计、costUnits |
| HydroSeek | 混合检索 | BM25+Dense+RRF 取舍 |
| linflux | 批处理引擎 | 虚拟线程、分表、幂等 |
| infra-kata | 基础三件套 | RPC 协议、LRU/击穿、限流熔断 |

## 3. 优化路线（按优先级）

### P0 一致性（本周可做完）
1. 全部服务统一：`/healthz` `/readyz` `/metrics` + Compose +（可选）`obs` profile  
2. 指标命名统一前缀与 label 规范（`*_total` / `*_latency_ms_count|sum|bucket`）  
3. 业务仓给出「组合调用」示例（谁调谁、如何计费/评测）

### P1 串联可演示（面试 demo 链）
```text
VoltSage.alert
  → FlowForge.run(plant-inspection)
  → ToolGate.create_work_order / search_manual
  → HydroSeek.search(manual)
  → PolyRoute.chat (可选 LLM 叙述)
  → Lumenscope.costByFeature() + RAGLens 评检索
```
交付：每仓 README「Integration」小节 + 一条 compose network 说明。

### P2 深度（深挖轮）
| 方向 | 做什么 |
|------|--------|
| VoltSage 知识库 | Keyword → HydroSeek HTTP 客户端，可 A/B |
| HydroSeek | 真实 embedding + rerank + RAGLens 评测集 |
| FlowForge | 持久化恢复 API / 演示 crash-recover |
| HarborCheck | 版面/表格抽取（docling 风格）+ 大样本回归 |
| infra-kata | 压测脚本与复杂度分析笔记（面试口算） |

### P3 打磨（投递前）
- Profile 只保留主讲 6 个，其余放「支撑能力」  
- 每个主讲仓：架构图、30s 话术、失败边界、指标截图  
- 与 JD 对齐裁剪（Java 后端强调 FlowForge/linflux/infra-kata；AI 应用强调 VoltSage/HarborCheck/RAGLens）

## 4. 不做的事

- 不把精读 clone 放回 GitHub  
- 不再开第 11 个「又一个 ChatBot / 后台 CRUD」  
- 不为堆语言而换栈；新语言只用于补齐协议面（如 TS ToolGate）

## 5. 投递叙事（30 秒）

> 我把 LLM 应用拆成网关(PolyRoute)、评测(RAGLens)、成本(Lumenscope)、业务 Agent(VoltSage)、单证管道(HarborCheck)、编排(FlowForge)、工具面(ToolGate)、检索(HydroSeek)，全部可 Docker 启动并暴露 Prometheus 指标，对应能源/物流真实场景，而不是 demo chatbot。
