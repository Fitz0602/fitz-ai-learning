# learning/ 目录指针 · 给 AI 读

> **此文件是 AI 必读的导航文件**。Fitz 看 INDEX.html，AI 读这个 MAP.md。
> 任何修改 learning/ 内容前，先读此文件理解项目架构。
> 最后更新: 2026-05-19（v4 重构：T1 精简 14 章，T2 全新 8 章，两轨交替）

---

## 0. 贯穿主线（知识体系的第一性原理）

整个学习计划由**一条逻辑链**贯穿，T1 和 T2 是同一条链的前后半段：

```
问题1: 信息如何进入模型？
  → T1 D1: 文本→Token→向量→位置感知→长上下文

问题2: 模型内部如何处理？
  → T1 D2: Attention提取关联 → FFN存储知识 → MoE按需激活

问题3: 模型如何学会"对"的行为？
  → T1 D3: 预训练建世界观 → SFT教格式 → RLHF/DPO对齐价值

问题4: 训练好的模型如何高效输出？
  → T1 D4: KV Cache加速 → 量化压缩 → Serving调度

    ↓ 以上是"一个聪明的模型"，以下是"一个可以做事的系统" ↓

问题5: 如何让模型主动行动？
  → T2 A1: Agent Loop循环 + Tool Use连接现实世界 + MCP标准化工具

问题6: 如何让模型想清楚再行动？
  → T2 A2: CoT推理链 → o1/R1机制 → Planning任务分解 → 反思闭环

问题7: 如何管好模型能"看到"什么？
  → T2 A3: Prompt→Context→Memory三层演进 + 渐进式披露

问题8: 如何让系统可靠运行？
  → T2 A4: Harness六组件 + Multi-Agent编排 + AgentOps可观测性
```

每一章在"主线连接"句中明确回答：**这章知识如何服务于上一级问题？**

---

## 1. 顶层结构

```
learning/
├── PLAN.md                    # 学习计划主文档（人/AI 都读）
├── MAP.md                     # 本文件 · AI 专用项目指针
├── llm-systems/               # T1 LLM 系统（已启动）
│   ├── INDEX.html             # 给 Fitz 看的可视化入口（不要 AI 直读）
│   ├── PROGRESS.md            # 详细进度表（v4 重构后 14 章）
│   ├── 1-input/               # D1 输入侧（全部完成）
│   │   ├── 1.1-tokenization/  ✅
│   │   ├── 1.2-embedding/     ✅
│   │   ├── 1.3-positional-encoding/ ✅
│   │   └── 1.4-long-context/  ✅
│   ├── 2-architecture/        # D2 模型骨架（3 章）
│   │   ├── 2.1-attention/     ✅（完整章节 + Quiz，2026-05-19）
│   │   ├── 2.2-multihead-variants/ ✅（完整章节 + Quiz，2026-05-20）
│   │   └── 2.3-ffn-moe/       ⏭ 下一章
│   ├── 3-training/            # D3 训练流水线（2 章精简）
│   │   ├── 3.1-pretrain-sft/  # 预训练+SFT 合并
│   │   └── 3.2-rlhf-dpo/      # RLHF·DPO·RL推理对齐
│   ├── 4-inference/           # D4 推理与部署（2 章精简）
│   │   ├── 4.1-inference-kvcache/ # 推理流程+KV Cache 合并
│   │   └── 4.2-quantization-serving/ # 量化+Serving 合并
│   ├── 5-infra/               # D5 基础设施（仅 deep-dives，无独立章）
│   │   └── deep-dives/
│   │       ├── 5-d1-gpu-memory-agent-cost.html  # GPU显存与Agent成本
│   │       └── 5-d2-scaling-law-product.html    # Scaling Law与产品决策
│   └── 6-eval/                # D6 评测与对齐（2 章精简）✅（全部完成，2026-05-20）
│       ├── 6.1-benchmark-judge/ ✅（完整章节 + Quiz，2026-05-20）
│       └── 6.2-alignment-hallucination/ ✅（完整章节 + Quiz，2026-05-20）
├── agent-engineering/         # T2 Agent 工程（全新建立，8 章）
│   ├── INDEX.html             # T2 知识图谱入口
│   ├── PROGRESS.md            # T2 进度表
│   ├── A1-loop-tools/         # A1 基础机制
│   │   ├── A1.1-agent-loop-react/    # Agent Loop + ReAct + Tool Use
│   │   └── A1.2-mcp-skills/          # MCP协议 + Tools vs Skills对比
│   ├── A2-reasoning-planning/ # A2 推理规划
│   │   ├── A2.1-cot-reasoning-o1/    # CoT + o1/R1机制 + Test-time Compute
│   │   └── A2.2-planning-reflection/ # Planning + 任务分解 + 反思循环
│   ├── A3-context-memory/     # A3 上下文与记忆
│   │   ├── A3.1-prompt-context-eng/  # Prompt→Context Engineering
│   │   └── A3.2-memory-system/       # Memory机制（短/长/外部/KG）
│   └── A4-harness-multiagent/ # A4 Harness工程
│       ├── A4.1-harness-six-components/ # Harness六组件 + Fitz框架对比
│       └── A4.2-multiagent-ops/       # Multi-Agent + Subagent + AgentOps
├── papers/                    # T3 论文精读（按需建）
├── vibe-coding/               # T4 Vibe Coding（按需建）
├── internal-radar/            # T5 司内雷达（按需建）
├── notes/                     # 追问/复盘/日志
│   ├── _automation-log.md     # 每日 automation 执行记录
│   └── {YYYY-MM-DD}-weekly-review.md
├── daily/                     # 已废弃，禁用
└── quiz/                      # 已废弃，禁用
```

---

## 2. 命名规范（铁律）

### 2.1 章节内文件（v2.3 简化，T1/T2 通用）

每个章节目录下**仅 2 个核心文件**：

| 文件类型 | 命名格式（T1） | 命名格式（T2） |
|---------|-------------|-------------|
| 章节内容 | `{D}.{C}-{slug}-chapter.html` | `A{n}.{m}-{slug}-chapter.html` |
| 章节 Quiz | `{D}.{C}-{slug}-quiz.html` | `A{n}.{m}-{slug}-quiz.html` |
| deep-dive | `deep-dives/{D}.{C}-d{n}-{slug}.html` | `deep-dives/A{n}.{m}-d{n}-{slug}.html` |

示例：
- `2.1-attention-chapter.html`
- `A1.1-agent-loop-chapter.html`

> ⚠️ 不再生成 1.2.1-is.html 这种节级独立文件。5 节是 chapter.html 内部 anchor。

### 2.2 5 节 anchor 结构（每章必须包含）

| 节序 | anchor id | 内容定位 |
|-----|-----------|---------|
| ① 是什么 | `#is` | 直觉建立 + 产品视角动机 |
| ② 怎么实现 | `#how` | 机制 + 流程图 + 实例 |
| ③ 为什么 | `#why` | 第一性原理 + 设计取舍 |
| ④ 演进与对比 | `#evolution` | 2024-2026 各流派 |
| ⑤ 与产品连接 | `#connect` | 串到 DDAgent / KBA / 跨境支付 |

每节必须有**主线连接句**（该节知识如何服务于贯穿主线的哪个问题）。

---

## 3. 学习进度（实时记录）

### 3.1 总进度
- T1 LLM 系统：70/70 节（100%，基于精简后 14 章×5 节=70 节，T1 全部完成 🎉）
- T2 Agent 工程：25/40 节（63%，8 章×5 节=40 节）
- T3-T5：未启动

### 3.2 T1 章节级进度（v4 精简架构）

| 章节 ID | 名称 | 状态 | 5节进度 | Quiz | 主线连接 |
|--------|------|------|--------|------|---------|
| **1.1** | Tokenization | ✅ 完成 | 5/5 | ✅ | 信息输入：文本→Token ID |
| **1.2** | Embedding | ✅ 完成 | 5/5 | ✅ | 信息输入：Token→语义向量 |
| **1.3** | 位置编码 | ✅ 完成 | 5/5 | ✅ | 信息输入：保留顺序信息 |
| **1.4** | 长上下文扩展 | ✅ 完成 | 5/5 | ✅ | 信息输入：扩展记忆边界 |
| **2.1** | Attention 机制 | ✅ 完成 | 5/5 | ✅ | 模型处理：Token如何动态关注彼此 |
| **2.2** | 多头变种 GQA/MQA/Flash | ✅ 完成 | 5/5 | ✅ | 模型处理：长上下文推理成本的根因 |
| **2.3** | FFN + 归一化 + MoE | ✅ 完成 | 5/5 | ✅ | 模型处理：知识存储与专家激活 |
| **3.1** | 预训练 + SFT | ✅ 完成 | 5/5 | ✅ | 训练对齐：建世界观+教指令格式 |
| **3.2** | RLHF · DPO · RL推理 | ✅ 完成 | 5/5 | ✅ | 训练对齐：塑造行为价值观→Agent品味判断力理论基础 |
| **4.1** | 推理流程 + KV Cache | ✅ 完成 | 5/5 | ✅ | 推理部署：KV Cache是Context工程的物理约束 |
| **4.2** | 量化蒸馏 + Serving | ✅ 完成 | 5/5 | ✅ | 推理部署：Agent成本控制基础 |
| **5-dd** | D5 deep-dives（附录） | ✅ 完成 | — | — | 信息补充：GPU成本 + Scaling Law |
| **6.1** | Benchmark + LLM-as-Judge | ✅ 完成 | 5/5 | ✅ | 评测：如何判断模型/Agent好坏 |
| **6.2** | 安全对齐 + 幻觉 | ✅ 完成 | 5/5 | ✅ | 评测：行为不稳定的根因 → Harness安全层动机 |

### 3.3 T2 章节级进度（全新）

| 章节 ID | 名称 | 状态 | 主线连接 | 前置 T1 |
|--------|------|------|---------|--------|
| **A1.1** | Agent Loop · ReAct · Tool Use | ✅ 完成 | 5/5 | ✅ | 模型→系统：从单次输出到循环执行 | T1 D2 后 |
| **A1.2** | MCP协议 · Tools vs Skills | ✅ 完成 | 5/5 | ✅ | 工具标准化 + Skills渐进式披露 | T1 D2 后 |
| **A2.1** | CoT · o1/R1 · Test-time Compute | ⏭ 下一章 | — | — | 推理能力：多想一步的系统工程 | T1 D3 后 |
| **A2.2** | Planning · 任务分解 · 反思 | ⬜ | 规划能力：DDAgent多步尽调实例 | T1 D3 后 |
| **A3.1** | Prompt→Context Engineering | ⬜ | 信息管理：100:1 Token比例与成本 | T1 D4 后 |
| **A3.2** | Memory机制（四层架构） | ⬜ | 状态持久：KBA项目经历的理论化 | T1 D4 后 |
| **A4.1** | Harness六组件 · Fitz框架对比 | ✅ 完成 | 系统可靠：原创框架 vs 行业实践 | T1 D6 后 |
| **A4.2** | Multi-Agent · Subagent · AgentOps | ⏭ 下一章 | 系统扩展：从Demo到Production | T1 D6 后 |

### 3.4 学习顺序（两轨交替）

```
T1 D1 ✅ → T1 D2（2.1→2.2→2.3）✅ → T2 A1（A1.1✅+A1.2✅）→
T1 D3（3.1→3.2）→ T2 A2（A2.1+A2.2）→
T1 D4（4.1→4.2）→ T2 A3（A3.1+A3.2）→
T1 D6（6.1→6.2）→ T2 A4（A4.1+A4.2）→
D5 deep-dives（附录，随时补充）
```

> 每完成一个 T1 领域，立刻在 T2 中找到对应的 Agent 应用节点，形成知识闭环。

### 3.5 Deep-dives 列表

| 路径 | 主题 | 来源 |
|------|------|------|
| `1-input/1.1-tokenization/deep-dives/1.1-d1-deployment-anatomy.html` | 大模型部署文件解剖 | 2026-05-14 追问 |
| `1-input/1.1-tokenization/deep-dives/1.1-d2-academic-audit.html` | Tokenizer 章节 vs 学术工业共识审计 | 2026-05-15 |
| `1-input/1.2-embedding/deep-dives/1.2-d2-academic-audit.html` | Embedding vs 2025-2026 学术工业共识审计 | 2026-05-15 |

---

## 4. 规则与铁律（AI 必须遵守）

### 4.0 审计必须强制 WebSearch

**铁律**：
1. 任何涉及"学术共识""最新研究""前沿对齐"的产出，**必须**先用 WebSearch + WebFetch 拉取权威资料
2. 信息源优先级：① 国内头部（Qwen/DeepSeek/智谱/智源）→ ② 国际头部（Google/Anthropic/OpenAI/Cohere）→ ③ 顶级会议论文仅补充
3. 引用论文必须给完整时间戳（如 "arxiv 2505.14178 / 2025-05"）
4. 发现冲突时**主章节立即修订**，不要只记入待办

### 4.1 生成新章节时

1. **必须先读 MAP.md 和 PROGRESS.md** 确定写哪章、写哪轨
2. **chapter.html 必须含主线连接句**（header 区标注，格式："主线连接：[本章在信息链上的位置]"）
3. **chapter.html 必须含极简一览图**（header 结束后紧接，见 §4.6 规范）
4. **chapter.html 必须含 5 节 anchor**（#is/#how/#why/#evolution/#connect）
5. **chapter.html 必须含导航按钮**（见 §4.8 规范：tag-row 内 `← 知识图谱` + `Quiz →`，底部 footer 导航条）
6. **必须更新本 MAP.md** 的"3. 学习进度"小节
7. **必须更新对应轨道的 PROGRESS.md**
8. **必须更新对应轨道的 INDEX.html**
9. T1 D5 不生成独立章节，仅生成 deep-dives

### 4.2 生成章节时必须 WebSearch（P0 铁律）

每次生成章节前，**必须用 WebSearch 搜索 3 次以上**，获取 2024-2026 权威最新资料：
- 搜索词示例：`"{主题} 2025 2026 state of art"`、`"Anthropic/DeepSeek/Google {主题} latest"`
- **禁止仅靠模型内置知识生成章节内容**（知识截止日前的内容不代表最新实践）
- T2 Agent 工程章节：必须搜索 Anthropic/OpenAI/LangChain 最新博客和技术报告

### 4.3 修改已有内容时

1. 修改文件名时，**必须搜索全部引用**并同步修改
2. INDEX.html 的章节卡片链接用完整相对路径

### 4.4 废弃路径警告

以下两个目录**已废弃**，永不要往里写新文件：
- `learning/daily/`
- `learning/quiz/`

### 4.5 知识沉淀触发

某章节满 5 节 + chapter.html + quiz.html 全部完成时，主动同步到：
- `/Users/fitzfei/WorkBuddy/.codebuddy/knowledge/llm-systems.md`
- `/Users/fitzfei/WorkBuddy/.codebuddy/knowledge/ai-product.md`

### 4.6 章节一览图规范（v1.0）

每个 chapter.html 必须在 header `</div>` 之后、`§① 是什么` section 之前插入**极简一览图**：

```html
<!-- ====== 章节一览图 ====== -->
<div class="diagram" style="margin:24px 0 8px;">
<p style="font-size:12px;font-weight:500;color:var(--muted);margin:0 0 10px;">章节一览 · 5节脉络速览</p>
<svg viewBox="0 0 680 340" width="100%" xmlns="http://www.w3.org/2000/svg" overflow="visible">
  <!-- 5个节点 + 箭头连接 -->
  <!-- 节点颜色：① 紫 EEEDFE/#534AB7，② 蓝 E6F1FB/#185FA5，③ 琥珀 FAEEDA/#BA7517，④⑤ 并排 -->
  <!-- marker id 用 ov-arr + 章节序号，如 ov-arr21（2.1章），防止多章共页时冲突 -->
  <!-- SVG 铁律：无 HTML 标签，每个 text 必须有 fill -->
</svg>
</div>
```

### 4.7 chapter.html 主线连接句规范

每个 chapter.html 的 header 区（副标题下方）必须包含：

```html
<div class="spine-link" style="font-size:12px;color:var(--purple);background:var(--purple-bg);padding:6px 12px;border-radius:6px;margin-top:8px;display:inline-block;">
  主线连接：[本章在信息链中回答的核心问题，≤30汉字]
</div>
```

### 4.8 chapter.html 导航按钮规范（v1.0，2026-05-20 新增）

**每个 chapter.html 必须包含两处导航**，缺一不可：

**① header 内 tag-row 末尾加两个按钮（CSS 中必须有 `.nav-link` 样式）：**

```html
<!-- CSS 中加入（放在 </style> 前）-->
.nav-link{font-size:12px;color:var(--purple);text-decoration:none;border:1px solid var(--purple);padding:3px 10px;border-radius:12px;font-weight:500;white-space:nowrap}
.nav-link:hover{background:var(--purple);color:#fff}
.chapter-footer{margin-top:48px;padding:16px 20px;background:var(--purple-bg);border-radius:10px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:10px}
.chapter-footer a{color:var(--purple);text-decoration:none;font-size:13px;font-weight:500}

<!-- tag-row 末尾加两个链接 -->
<a href="../../INDEX.html" class="nav-link" style="margin-left:auto;">← 知识图谱</a>
<a href="{D}.{C}-{slug}-quiz.html" class="nav-link">Quiz →</a>
```

> 注意：`href` 中 `../../INDEX.html` 是从章节目录（`{D}-xxx/{D}.{C}-slug/`）出发两级返回 `llm-systems/INDEX.html` 的相对路径，T2 章节同理。

**② `</body>` 前加底部 footer 导航条：**

```html
<div class="chapter-footer">
  <a href="../../INDEX.html">← 返回知识图谱</a>
  <a href="{D}.{C}-{slug}-quiz.html">📝 去做 Quiz（10 题）→</a>
</div>
```

> ⚠️ 已知问题（2026-05-20 修复）：2.2 / 6.1 / 6.2 章节生成时遗漏了此规范，已手动补全。后续新章节必须从模板开始就包含上述两处导航。

---

## 5. 自动化引用

- **automation id**: `automation-1778760935083`
- **触发**: 每天 12:00（含周末）
- **prompt 版本**: v4.0（两轨交替，T1/T2 各章按顺序，必须 WebSearch 权威信息源）
- 每次执行后必须在 `notes/_automation-log.md` 追加记录
- **手动触发**：Fitz 可随时要求"按照 MAP 生成下一章"，AI 读 MAP.md 的"学习顺序"确定下一章

---

## 6. 给 AI 的下次填充建议

**D2 已完成（2026-05-21）：2.1 Attention ✅ + 2.2 多头变种 ✅ + 2.3 FFN+归一化+MoE ✅**
**T2 A1.1 已完成（2026-05-21）：Agent Loop · ReAct · Tool Use ✅**
**T2 A1.2 已完成（2026-05-22）：MCP协议 · Tools vs Skills ✅**

**4.1 已完成（2026-05-25）：推理流程+KV Cache ✅ — D4 开篇！**
**4.2 已完成（2026-05-26）：量化蒸馏+Serving ✅ — D4 收官！T1 全部完成！**
**D5 deep-dives 已完成（2026-05-26）：GPU成本 + Scaling Law ✅**

**下一章**：T2 A4.2 Multi-Agent · Subagent · AgentOps（A4.1 已完成 ✅）

必须 WebSearch 的关键词：
- `"multi-agent orchestration patterns 2025 2026 production LangGraph CrewAI"`
- `"agent observability tracing OpenTelemetry 2026 Langfuse"`
- `"subagent delegation supervisor pattern AI agent production"`

主线连接句：`"系统扩展：从Demo到Production的工程跨越"`

---

## 7. SVG 流程图铁律（详见原版，不变）

> P0: SVG 中绝对禁止 `<b>`/`<strong>`/`<em>`/`<div>`/`<span>`/`<p>`/`<br>`，用 `<tspan font-weight="700">` 替代
> P1: 每个 `<text>` 必须有显式 `fill`；viewBox 安全余量 ≥ 20px
> P2: 超大 SVG 加 `overflow="visible"`；marker orient 用 `"auto"`

### 7.8 SVG vs HTML 选型铁律

**唯一判断问题：把内容打散重排，意义会丢失吗？**
- 会丢失 → 用 SVG（流程图、架构图、时间线、空间隐喻）
- 不会丢失 → 用 HTML（表格、列表、段落、标签徽章）

**推荐架构：SVG 骨架 + HTML 详情卡片**
- SVG 只画"流程骨架"，`<text>` 元素永远不超过 30 个
- 详情拆出来作为独立 HTML 卡片（`<table>` / `.card`）

### 7.10 数学公式渲染

所有含 LaTeX 公式的章节，`<head>` 必须加载 KaTeX：

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.css">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.js"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/contrib/auto-render.min.js"
        onload="renderMathInElement(document.body, {delimiters: [{left:'$$',right:'$$',display:true},{left:'$',right:'$',display:false}], throwOnError:false});"></script>
```
