# Fitz AI 学习计划 v3.0

> **创建**: 2026-05-14 | **重构**: 2026-05-19（v3 对齐 DeepSeek Agent PM JD + 贯穿逻辑链）
> **形态**: 长期学习仪式（非项目）
> **每日投入**: 30min 阅读 + 10min Quiz + 不限时追问

> ⚠️ **AI 必读 `learning/MAP.md`** — 项目结构、命名规范、进度记录、铁律全在那
> 本文件聚焦"为什么这样学"和"怎么协作"，结构性细节去 MAP.md
> **目标档位**: 先 A 后 B
> - **档位 A**（必达）: 与一线 AI 研究员同频对话——读懂论文、理解架构、能讨论 Agent 系统设计
> - **档位 B**（可选）: 不排除转研究方向——需补数学 + 动手实操

---

## 一、贯穿主线（最重要的一条线）

整个学习计划由一条逻辑链贯穿，T1 LLM 系统和 T2 Agent 工程是同一条**信息流动链**的前后半段：

```
信息进入模型 → 模型处理信息 → 训练使行为对齐 → 高效推理部署
       ↓
让模型主动行动 → 让模型想清楚 → 管理模型看到什么 → 系统可靠运行
```

每一章的学习都在回答这条链上的某个关键问题。**LLM 原理回答"模型能力上限"，Agent 工程回答"系统可靠性上限"**，两者缺一不可。

---

## 二、协作分工（铁律）

| 角色 | 职责 | 不做 |
|------|------|------|
| **AI** | 找权威资料/拆晦涩文本/做 HTML/出 Quiz/批改/深挖追问/沉淀知识库 | 不替你思考、不替你下判断 |
| **Fitz** | 每天 40min 投入、追问质疑、提供领域反馈、决定深挖方向 | 不需自己找资料、不需自己整理笔记 |

---

## 三、每日学习闭环

```
[T-1 12:00 · automation 或 Fitz 手动触发]
  → 读 MAP.md 确定下一章（T1/T2 交替顺序）
  → WebSearch 3+ 次获取权威信息源
  → 生成整章 chapter.html（含一览图+主线连接句+5节全写）
  → 生成 quiz.html（10 题）
  → 更新 MAP.md / PROGRESS.md / INDEX.html / _automation-log.md

[早晨/通勤 · Fitz 阅读 30min]
  → 打开 INDEX.html 或直接进章节阅读
  → 看不懂/想深挖随时问，AI 现场拆解+画图+举例

[午间/碎片 · Quiz 10min]
  → 完成 10 题，AI 批改 + 解释错点

[任意时间 · 追问与沉淀]
  → 触发 deep-dive 时，新增到该章节 deep-dives/ 子目录
  → 章节完整学完时同步到 .codebuddy/knowledge/
```

> **手动触发生成**：Fitz 可随时说"按照 MAP 生成下一章"，AI 读 MAP.md 中的学习顺序决定写哪章。不受 automation 时间限制。

---

## 四、5 条学习轨道

| 轨道 | 知识库路径 | 状态 |
|------|----------|------|
| **T1 LLM 系统** 🟣 | `learning/llm-systems/` | ✅ 启动（D1 全完，D2 进行中） |
| **T2 Agent 工程** 🟢 | `learning/agent-engineering/` | ✅ 目录建立，A1 待启动 |
| **T3 论文精读** 🟡 | `learning/papers/` | ⏳ 按需建 |
| **T4 Vibe Coding** 🔵 | `learning/vibe-coding/` | ⏳ 按需建 |
| **T5 司内雷达** 🟤 | `learning/internal-radar/` | ⏳ 按需建 |

---

## 五、T1 LLM 系统 · 精简 14 章路线

| 领域 | 章节（v4 精简）| 主线问题 |
|------|-------------|---------|
| **D1 输入侧** ✅ | 1.1 Tokenization / 1.2 Embedding / 1.3 位置编码 / 1.4 长上下文 | 文本如何变成模型能消费的向量序列？ |
| **D2 模型骨架** | 2.1 Attention / 2.2 多头变种 / **2.3 FFN+MoE（合并）** | Transformer 中间发生了什么？ |
| **D3 训练（精简）** | **3.1 预训练+SFT（合并）** / 3.2 RLHF·DPO·RL推理 | 模型如何学会"对"的行为？ |
| **D4 推理部署（精简）** | **4.1 推理流程+KV Cache（合并）** / **4.2 量化+Serving（合并）** | 训练好的模型如何高效运行？ |
| **D5 基础设施** | ~~独立章节~~ → 2 篇 deep-dive 附录 | GPU/Scaling Law 作为背景知识 |
| **D6 评测对齐（精简）** | **6.1 Benchmark+Judge（合并）** / **6.2 对齐+幻觉（合并）** | 模型/Agent 好不好用怎么判断？ |

> **精简逻辑**：D5 基础设施（GPU/并行/框架）对 Agent PM 没有决策杠杆，砍掉独立章；D3/D4/D6 合并减少重复，聚焦最有产品决策价值的原理。

---

## 六、T2 Agent 工程 · 全新 8 章路线

| 领域 | 章节 | 主线问题 | 前置 T1 章节 |
|------|------|---------|------------|
| **A1 基础机制** | A1.1 Agent Loop·ReAct·Tool Use / A1.2 MCP·Skills | 如何让模型主动行动？ | T1 D2 后 |
| **A2 推理规划** | A2.1 CoT·o1/R1·推理链 / A2.2 Planning·反思 | 如何让模型想清楚再行动？ | T1 D3 后 |
| **A3 上下文记忆** | A3.1 Prompt→Context Engineering / A3.2 Memory 四层架构 | 如何管好模型能"看到"什么？ | T1 D4 后 |
| **A4 Harness 工程** | A4.1 Harness六组件·Fitz框架对比 / A4.2 Multi-Agent·AgentOps | 如何让系统可靠运行？ | T1 D6 后 |

> **Harness 六组件（2026 前沿）**：意图建模 + 上下文记忆 + 工具执行环境 + 多Agent编排 + 评估反馈闭环 + 治理运维。A4.1 章节将 Fitz 原创框架与行业实践做系统对比。

---

## 七、知识入库（跨项目长期沉淀）

每个章节学完后，核心结论沉淀到：
- LLM 系统知识 → `/Users/fitzfei/WorkBuddy/.codebuddy/knowledge/llm-systems.md`
- 概念框架级 → `/Users/fitzfei/WorkBuddy/.codebuddy/knowledge/ai-product.md`
- 司内信息 → `/Users/fitzfei/WorkBuddy/.codebuddy/knowledge/internal-ai-radar.md`

---

## 八、自动化

- **automation id**: `automation-1778760935083`
- **名称**: Fitz AI 学习计划 · 每日整章生成 v4
- **触发**: 每天 12:00（含周末）
- **职责**: 读 MAP.md 确定下一章（T1/T2 交替），WebSearch 权威资料，生成整章 HTML + 10 题 Quiz，同步 4 处进度
- **手动触发**: Fitz 说"按 MAP 生成下一章"即可，不受时间限制

---

## 九、当前状态（2026-05-19）

- ✅ T1 D1 输入侧全部完成（4 章 20 节）
- ✅ T2 agent-engineering/ 目录骨架已建立
- ✅ 学习计划 v4 架构确定（14+8=22 章，贯穿逻辑链，两轨交替）
- ⏭ 下一章：T1 2.1 Attention 机制

---

*v3.0 重构: 2026-05-19 | 对齐 DeepSeek Agent PM JD + 2026 前沿趋势*
