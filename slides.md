---
theme: default
title: "AI Slides Open Loop"
info: |
  用 Slidev 复刻开放、可控、可验证的 AI PPT 生成闭环
drawings:
  persist: false
transition: slide-left
mdc: true
---
# AI Slides Open Loop

<div class="open-loop-subtitle">用 Slidev 复刻开放、可控、可验证的 AI PPT 生成闭环</div>

<div class="open-loop-meta">Dapeng Lab · 2026-05-09</div>

<!-- 从 Manus Slides 的黑盒机制，到 Slidev 的开放复刻。 -->
<!--
Slide 1: 从 Manus Slides 的黑盒机制，到 Slidev 的开放复刻。
-->

---

# 问题：AI PPT 不能只是一次性生成

<div class="open-loop-summary">真正可用的 AI PPT 系统需要可编辑、可预览、可导出、可验证。</div>

- 二进制 PPTX 难以被 Agent 精确 diff 和增量修复
- 纯 HTML 托管缺少项目生命周期和导出闭环
- 黑盒平台能力强，但迁移和调试成本高
<!--
Slide 2: 真正可用的 AI PPT 系统需要可编辑、可预览、可导出、可验证。
-->

---

# Manus 给出的工程启示

<div class="open-loop-summary">Manus Slides 的关键不是某个开源框架，而是 artifact 生命周期。</div>

- 文件层：slide_state.json + 每页 HTML
- 注册层：available slide projects 白名单
- 预览层：slide_present 返回 manus-slides:// 链接
- 状态层：只有 edited slide 才能进入预览
<!--
Slide 3: Manus Slides 的关键不是某个开源框架，而是 artifact 生命周期。
-->

---

# 开放复刻：Slidev + Registry + Sandbox

用公开工具复刻 Manus 的工程思想，而不是复刻私有协议。

```mermaid
flowchart LR
  A[AI Outline] --> B[slides.md]
  B --> C[Slidev Dev Preview]
  B --> D[Slidev Build]
  D --> E[Static Preview]
  B --> F[Export PDF PNG PPTX]
  C --> G[Registry]
  D --> G
  F --> G
  G --> H[Verification Report]
```
<!--
Slide 4: 用公开工具复刻 Manus 的工程思想，而不是复刻私有协议。
-->

---

# 开放 Registry：把白名单变成透明元数据

我们保留注册层，但不做隐藏状态。

| 字段 | 作用 | Manus 对照 |
| --- | --- | --- |
| project_id | 项目身份 | presentation/project id |
| project_dir | 可迁移路径 | project_dir |
| entry | Slidev 源文件 | 每页 HTML + state |
| preview_url | 本地或沙箱预览 | manus-slides:// |
| exports | PDF/PNG/PPTX 产物 | 附件导出 |
<!--
Slide 5: 我们保留注册层，但不做隐藏状态。
-->

---

# 验证闭环：让生成结果可被机器检查

<div class="open-loop-summary">AI 生成之后，系统必须能自己判断产物是否可用。</div>

- 校验 outline 与 slides.md 页数一致
- 校验资源路径存在且可读取
- 构建 dist 并启动静态预览
- 截图检查非空画面
- 导出 PNG/PDF/PPTX 并记录产物
<!--
Slide 6: AI 生成之后，系统必须能自己判断产物是否可用。
-->

---

# 结论：PPT 应该成为可执行工程对象

<div class="open-loop-summary">Slidev 让开放实现变得足够简单，Manus 让我们看清注册层的重要性。</div>

- Manus 证明了 Web Slides + 沙箱 + 注册层的产品价值
- Slidev 提供了开放、可迁移、可调试的实现底座
- AI 负责生成结构化内容，代码负责验证和交付
<!--
Slide 7: Slidev 让开放实现变得足够简单，Manus 让我们看清注册层的重要性。
-->

<style>
:root {
  --open-loop-accent: #2563eb;
  --open-loop-secondary: #16a34a;
  --open-loop-background: #f8fafc;
}
.slidev-layout { background: var(--open-loop-background); }
.slidev-layout h1 { color: #0f172a; letter-spacing: 0; }
.open-loop-subtitle { font-size: 1.6rem; line-height: 1.35; color: var(--open-loop-accent); margin-top: 1rem; max-width: 820px; }
.open-loop-meta { margin-top: 2rem; color: #475569; font-size: 1rem; }
.open-loop-summary { color: #475569; margin: 0.5rem 0 1.25rem; font-size: 1.1rem; }
.slidev-layout li { margin: 0.55rem 0; }
.slidev-layout table { font-size: 0.95rem; }
.slidev-layout th { color: white; background: var(--open-loop-accent); }
.slidev-layout td { background: rgba(255,255,255,0.72); }
</style>
