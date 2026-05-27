# 自动化执行日志

> 每次 automation 运行后追加一行；Fitz 可随时翻看

## 格式
```
[YYYY-MM-DD HH:MM] 轨道 · 主题 · 产出物 · 复习触发?/沉淀触发?
```

---

## 记录

[2026-05-14 20:14] manual · T1 W1 D1 Tokenizer · daily/2026-05-15-T1-tokenizer-day1.html + quiz/2026-05-15.md · 首次启动，无复习无沉淀
[2026-05-14 20:34] manual-update · T1 W1 D1 Tokenizer · 追加章节4.5 切词流程图（贪心匹配SVG + 5个实例：英文/拼错/数字/中文/emoji）· 基于Fitz追问深化
[2026-05-14 20:45] note-deep-dive · LLM部署解剖 · notes/2026-05-14-llm-deployment-anatomy.html · 以DeepSeek-V3为例的4类文件架构图+依赖关系图+生命周期表，串联跨境支付产品视角
[2026-05-14 21:00] migration-v2.1 · 知识库重构 · 建 learning/llm-systems/{INDEX.html, PROGRESS.md, 6领域20章节空目录} · 迁入 1.1-tokenization/{chapter.html, deep-dives/llm-deployment-anatomy.html} · 清空旧 daily/ 与 notes/ 中的孤立文件 · 更新 automation prompt 至 v2.1（章节填充模式）
[2026-05-15 10:09] manual-update · v2.2 升级 · 新增 1.1-tokenization/quiz.html（交互式5题，章节内可达） · INDEX 章节卡片加 Quiz 按钮 · chapter.html 顶部加 Quiz 入口 · 删除旧 quiz/2026-05-15.md · automation prompt 升级到 v2.2（Quiz 改为章节内 HTML 形式）
[2026-05-15 10:25] manual-refactor · v2.2 命名规范化 · 重命名所有章节内文件加 ID 前缀（1.1-tokenization-chapter/quiz.html, deep-dives/1.1-d1-*）· INDEX 移除 Quiz 按钮（Quiz入口收回章节内部）· 修复 chapter.html 过期 quiz.md 引用 · 新建 learning/MAP.md（AI 专用项目指针）· 废弃 daily/ 和 quiz/ 加警示文件 · automation prompt 加入 MAP.md 必读
[2026-05-15 13:57] manual-run · 提前跑今日材料 · T1-1.2.1-is + T1-1.2 quiz 首版 · 产出 1.2-embedding/1.2.1-is.html + 1.2-embedding/1.2-embedding-quiz.html · automation 时间从 20:00 改为 12:00（明天起生效）· INDEX/PROGRESS/MAP 三处进度同步至 6/100
[2026-05-15 14:04] v2.3-refactor · 架构对齐 · Fitz 发现 1.1（合订本）vs 1.2（节级独立）不一致 · 选择"统一回到合订本"方案 · 操作: 1) mv 1.2.1-is.html → 1.2-embedding-chapter.html 2) chapter 加 5 节 anchor (is/how/why/evolution/connect)，已填的 ① + 4 个占位 3) 1.1 chapter 加 anchor + 5节进度导航 4) Quiz 返回链用 chapter.html#anchor 5) MAP/PROGRESS/automation prompt 全部升级到 v2.3 · 不再产生节级独立文件
[2026-05-15 15:14] manual-run · 1.2 Embedding 一次性补完 ②③④⑤ 4 节 + Quiz 升级覆盖 5 节 · 产出 1.2-embedding-chapter.html (5/5 节 ≈75min)、1.2-embedding-quiz.html (5 题覆盖 5 节) · INDEX 1.2 卡片 partial→done · 进度 6→10/100 · 下一章：1.3 位置编码
[2026-05-15 15:14] deep-dive-audit · 1.1 Tokenization vs 学术工业共识审计 · 产出 deep-dives/1.1-d2-academic-audit.html · 7 个改进点（缺失：BPE训练精确流程/pre-tokenization/信息论视角/glitch tokens/语言公平性/数字推理因果/多模态；偏差：BLT 时效）· 整体对齐度 87% · P0 待补：glitch tokens 安全攻击面 + tokenization→数字推理因果链
[2026-05-15 15:24] v2-refactor-with-real-search · Fitz 指出 v1 审计的论文都是 2023-2024 过时 · 用 WebSearch+WebFetch 拉取 2025-2026 最新进展 · 主章节 §② 重写：4 阶段流水线 SVG + cl100k_base 真实正则 + BPE 6 步训练 + merges 顺序优先级 · 主章节 §③ 重写：信息论 Zipf 定律 + 数字推理因果链（引 arxiv 2505.14178/NeurIPS 2025 spotlight 2506.19004/AAAI 2026 GlitchMiner）+ One-Hot 对比 · 审计文档 v2 重做（10 篇真实参考文献含时间戳）· 整体对齐度 87%→93% · 关键 SOP 制度化建议：审计必须强制 WebSearch
[2026-05-17 12:06] weekly-review · 周日特殊流程 · 产出 learning/notes/2026-05-17-weekly-review.md · 回顾W1全周进展（2章10节+3篇deep-dive+4次架构升级+3条铁律确立）· 下周计划：1.3位置编码#is + T2-T5轨道启动 · 进度不变仍10/100 · 无复习触发无沉淀触发
[2026-05-18 10:30] manual-fix + automation-cleanup · 诊断过去3天automation不落盘问题 · 根因：双重automation(id 1778760935083 设计为"不写文件")+ v2.4 prompt过长模型未完成写文件步骤 · 操作：删除重复automation / 手动补写1.3位置编码完整章节(5/5节≈80min) + quiz · WebSearch验证行业共识(Meta/Qwen/DeepSeek) · 进度 10→15/100 · INDEX/PROGRESS/MAP全部同步 · 下一章：1.4长上下文扩展
[2026-05-18 12:00] automation-1778760935083 · T1 1.4长上下文扩展 §① 是什么 · 产出 1.4-long-context-chapter.html (1/5节 ≈16min) + 1.4-long-context-quiz.html (10题) · WebSearch 4次(PI/NTK/YaRN/NSA/iRoPE) · 进度 15→16/100 · INDEX/PROGRESS/MAP/automation-log 四处同步
[2026-05-19 10:30] manual · T1 1.4长上下文扩展 §②③④⑤ 全部补全 · chapter.html 完整5节：PI原理/NTK-aware/YaRN三段策略+温度修正/iRoPE/NSA时间线/产品选型决策树 · quiz.html已有10题（上次生成）无需修改 · D1全部完成 · 进度16→20/100 · automation改为每天1整章，下一章2.1 Attention · INDEX/PROGRESS/MAP全部同步
[2026-05-19 14:44] automation-1778760935083 · T1 2.1 Attention 机制 完整章节 · 产出 2.1-attention-chapter.html (5/5节 ≈75min) + 2.1-attention-quiz.html (10题) · WebSearch 3次(MLA/GQA/FlashAttention权威资料) · D2开篇 · 进度 20→25/70(v4架构) · INDEX/PROGRESS/MAP/_automation-log 四处同步 · 下一章：2.2 多头变种 GQA/MQA/Flash
[2026-05-20 12:00] automation-1778760935083 · T1 2.2 多头变种 GQA/MQA/MLA/FlashAttention 完整章节 · 产出 2.2-multihead-variants-chapter.html (5/5节) + 2.2-multihead-variants-quiz.html (10题) · WebSearch 3次(GQA/MQA Qwen Llama / FlashAttention 3-4 / DeepSeek MLA MHA2MLA) · 权威信息源：Sebastian Raschka GQA 2026 分析 / arxiv 2502.14837 MHA2MLA ACL 2025 / FlashAttention-4 2026.03 发布 · 进度 25→30/70(43%) · INDEX/PROGRESS/MAP/_automation-log 四处同步 · 下一章：2.3 FFN+归一化+MoE
[2026-05-20 15:23] manual · T1 D6 评测与对齐 2 章全部完成（Fitz 手动触发跳过 D2 剩余先做 D6）· 产出 6.1-benchmark-judge-chapter.html + quiz.html / 6.2-alignment-hallucination-chapter.html + quiz.html · WebSearch 5次(Benchmark状态/LLM-as-Judge方法论/Agent评测框架/安全对齐/幻觉分类) · 权威信息源：Mason AI Lab / Confident.ai / 棱镜空间 / Calmops 2026 / OpenAI幻觉报告2025.09 / MSRA OPA-DPO CVPR2025 / Anthropic CA 2.0 · 进度 30→40/70(57%) · D6全部完成✅ · INDEX/PROGRESS/MAP/_automation-log 四处同步 · 下一章：2.3 FFN+归一化+MoE（回到 D2）
[2026-05-21 12:00] automation-1778760935083 · T1 2.3 FFN+归一化+MoE 完整章节 · 产出 2.3-ffn-moe-chapter.html (5/5节) + 2.3-ffn-moe-quiz.html (10题) · WebSearch 4次(SwiGLU演进/MoE专家路由/RMSNorm归一化/MoE 2025-2026模型对比) · 权威信息源：Sebastian Raschka LLM架构对比2026 / TensorOps MoE Field Guide 2026 / DeepSeek-V3无辅助损失均衡论文 · D2全部完成✅ · 进度 40→45/70(64%) · INDEX/PROGRESS/MAP/_automation-log 四处同步 · 下一章：T2 A1.1 Agent Loop·ReAct·Tool Use
[2026-05-22 13:35] automation-1778760935083 · T1 3.1 预训练+SFT 完整章节 · 产出 3.1-pretrain-sft-chapter.html (5/5节) + 3.1-pretrain-sft-quiz.html (10题) · WebSearch 3次(预训练SFT最新进展/数据配比工程/后训练三阶段流水线) · 权威信息源：Karpathy 2025年度回顾 / Meta Post-training 101 / CSDN现代LLM训练全景 / Sundeep Teki后训练指南2026 · D3开篇 · 进度 45→50/70(71%) · INDEX/PROGRESS/MAP/_automation-log 四处同步 · 下一章：T1 3.2 RLHF·DPO·RL推理对齐
[2026-05-25 12:00] automation-1778760935083 · T1 4.1 推理流程+KV Cache 完整章节 · 产出 4.1-inference-kvcache-chapter.html (5/5节) + 4.1-inference-kvcache-quiz.html (10题) · WebSearch 5次(PagedAttention/vLLM SGLang/DeepSeek DualPath/投机解码EAGLE-3/FlashInfer) · 权威信息源：vLLM SOSP 2023 / NVIDIA KVTC ICLR 2026 / LCA ACL 2026 / DeepSeek DualPath / Morph 2026 / FlashInfer MLSys 2025 · D4开篇 · 进度 60→65/70(93%) · INDEX/PROGRESS/MAP/_automation-log 四处同步 · 下一章：T1 4.2 量化蒸馏+Serving
[2026-05-27 12:00] automation-1778760935083 · T2 A4.1 Harness六组件·Fitz框架对比 完整章节 · 产出 A4.1-harness-six-components-chapter.html (5/5节) + A4.1-harness-six-components-quiz.html (10题) · WebSearch 3次(Harness Engineering Mitchell Hashimoto 2026/Agent reliability guardrails 2026/Multi-agent orchestration 2026) + WebFetch 2次(robonaissance.com/ybuild.ai) · 权威信息源：Mitchell Hashimoto 2026.02博客 / OpenAI Codex Harness Engineering 2026.02 / Anthropic Planner/Generator/Evaluator 2026.03 / LangChain TerminalBench 52.8→66.5% / Thoughtworks Fowler 2×2矩阵 2026.04 · A4开篇 · 进度 20→25/40(63%) · INDEX/PROGRESS/MAP/_automation-log 四处同步 · 下一章：T2 A4.2 Multi-Agent·Subagent·AgentOps
