# Hi, I'm ShengL1n

Java → Agent / RAG 工程师。在能源与物流业务里做可上线的 AI 系统，而不是 demo ChatBot。

## 项目

| 项目 | 栈 | 一句话 |
|------|----|--------|
| [PolyRoute](https://github.com/ShengL1n/PolyRoute) | Go + React | 企业级 LLM 网关：多模型路由、成本治理、RAG API、运维控制台 |
| [RAGLens](https://github.com/ShengL1n/RAGLens) | Python + React | 生产级 RAG 评测：IR + LLM Judge、Bad Case 工作台、回归对比 |
| [linflux](https://github.com/ShengL1n/linflux) | Java 21 | 有界批处理引擎：虚拟线程、分表游标、幂等、Redis Sink |
| [VoltSage](https://github.com/ShengL1n/VoltSage) | Java 21 | 光储运维智能体：遥测→可解释根因→手册检索→工单；Docker + 指标 |
| [HarborCheck](https://github.com/ShengL1n/HarborCheck) | Python | 物流单证三方核对：规则优先 + LLM 修复 + FastAPI + 指标 |
| [Lumenscope](https://github.com/ShengL1n/Lumenscope) | Node.js | LLM 成本/延迟归因：span、瀑布、按业务线出账 |
| [ai-chatbot-all](https://github.com/ShengL1n/ai-chatbot-all) | TS/Java | 全栈 AI 对话应用 monorepo |

## 技术栈

- **后端**：Java 21 · Spring · Go · Python · Node.js
- **AI 工程**：Agent 工具调用 · RAG 评测 · 多模型网关 · 成本可观测
- **中间件**：MySQL/PostgreSQL · Redis · 向量库 · 消息队列 · 分库分表
- **上线路径**：Docker Compose · Prometheus · Grafana · OpenAI 兼容网关

## 面试怎么用

1. 按 JD 选 1–2 个项目深讲：**业务问题 → 架构取舍 → 边界与指标**
2. 可上线项目可演示：`docker compose up` → `/metrics` → Grafana
3. 组合故事：网关(PolyRoute) + 评测(RAGLens) + 业务 Agent(VoltSage) + 单证核对(HarborCheck) + 成本归因(Lumenscope)
