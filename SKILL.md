---
name: codex-video-workflow
description: Use when creating product demo videos, feature walkthroughs, tutorial animations, or marketing video content without traditional editing software (Premiere, After Effects). Use when user says "做个产品视频", "代码做视频", "不用剪辑软件出视频", or needs pixel-perfect text/data in video scenes.
---

# Codex Video Workflow

> **核心理念**：不用 Premiere / After Effects，也能做出专业产品视频。
> 把「视觉确认」和「代码执行」拆成两步，用 AI 图片生成确认画面，用代码精确复刻动画。

## 适用场景

| 场景 | 说明 |
|------|------|
| 产品功能演示 | Dashboard、数据面板、SaaS 产品 walkthrough |
| 教学 / 教程视频 | 步骤展示、操作流程可视化 |
| 社交媒体短视频 | 产品亮点、功能发布 |
| 销售 / 营销素材 | 客户 pitch、方案展示 |

## 核心哲学

传统路径的问题：
1. **纯文字 prompt → AI 生视频**：模糊，无法精确控制文字、布局、数据
2. **传统剪辑软件**：学习成本高、价格贵、迭代慢

本方法的解法：**双层分离**

```
┌─────────────────────────────────────────┐
│          Image Layer（图片层）           │
│  AI 生成的纹理、插画、背景、氛围图       │
│  → 负责「感觉对不对」                   │
└──────────────────┬──────────────────────┘
                   │ 组合
┌──────────────────▼──────────────────────┐
│          Code Layer（代码层）            │
│  文字、数字、按钮、图表、动画序列        │
│  → 负责「精确不精确」                   │
└─────────────────────────────────────────┘
```

**关键原则**：
- 文字 / 数据 / 布局 → 必须用代码实现（Code Layer）
- 纹理 / 插画 / 氛围 → 可以用 AI 图片生成（Image Layer）
- 两层叠加 = 既有设计感，又有像素级精确

---

## 五步工作流

### Step 1：脚本分镜（Script & Storyboard）

为每个场景定义四个要素：

| 要素 | 说明 | 示例 |
|------|------|------|
| 📐 内容布局 | 元素、位置、数量 | 左侧环形图，右侧大号数字 |
| 🎭 情绪基调 | 张力、反差、转场感 | 「冷静而浪费」的临床感 |
| 📝 文字卡片 | 需要出现的标注文本 | "4.2 hrs/day wasted" |
| 🎬 动画序列 | 进场 → 停留 → 退场顺序 | 环形图先填充 → 数字淡入 → 标注滑入 |

**输出格式**：

```markdown
## Scene N: [场景名称]

**布局**：[描述主要元素和位置关系]
**基调**：[一句话描述情绪 / 氛围]
**文字元素**：
- 标题: "[文字内容]"
- 标注: "[文字内容]"
- 数据: "[文字内容]"
**动画序列**：
1. [第一个动画动作]
2. [第二个动画动作]
3. [第三个动画动作]
```

### Step 2：生成视觉预览（Visual Pre-Viz）

用 GPT-Image-2（或任何图片生成工具）为每个场景生成 **16:9 参考图**。

**Prompt 结构**（必须遵循）：

```
A [风格] [场景类型] in 16:9 landscape format.

Left section: [左侧元素精确描述，含颜色、大小]
Right section: [右侧元素精确描述]
Bottom: [底部元素]

Color palette: [具体色值或色系]
Overall tone: [情绪描述]
Typography: [字体风格，如 clean sans-serif, monospace]
```

**示例 Prompt**：

```
A clean dark analytics dashboard in 16:9 landscape format.

Left: large donut chart showing 70% in muted red (#b44040) against dark gray (#1a1a2e).
Right: "4.2 hrs" in large white text (48px equivalent), subtitle "wasted daily" in gray.
Bottom: thin progress bar, 3 small stat cards with icons.

Color palette: dark navy (#0f0f23), muted red (#b44040), white (#ffffff), gray (#8892b0)
Overall tone: clinical and quietly wasteful
Typography: clean sans-serif, monospace for numbers
```

**⚠️ 注意**：
- 图片中的文字**仅供参考**，最终文字由代码渲染
- 重点关注：色彩搭配、空间布局、视觉重心
- 每个场景生成 1-2 张候选图，选最接近的

### Step 3：代码复刻（Code Handover）

将预览图交给代码执行层（Codex / Claude / 手动编码），附带分层指令：

**Handover Prompt 模板**：

```markdown
请根据这张参考图实现一个浏览器可运行的动画场景。

## 分层规则
- **Code Layer**（代码实现）：所有文字、数字、按钮、图表、动画
- **Image Layer**（图片导入）：背景纹理、插画素材（如有）

## 技术要求
- 技术栈：HTML + CSS + JavaScript（或 React + Tailwind）
- 尺寸：1920×1080 (16:9)
- 动画：CSS animations / GSAP / Framer Motion
- 不要用 AI 生成图片，只根据参考图复刻 UI 和动画

## 动画序列
1. [具体动画步骤]
2. [具体动画步骤]
3. [具体动画步骤]

## 执行步骤
1. 先分析参考图的布局结构
2. 实现静态 UI
3. 添加动画序列
4. 确保可在浏览器中独立运行
```

### Step 4：迭代调优（Iterative Refinement）

对比代码输出与原始预览图，提供**具体、客观**的修改指令：

**✅ 正确的反馈方式**：
```
- 环形图颜色改为 #b44040，当前太亮了
- 标注文字在主内容淡入后再滑入，延迟 0.5s
- 右侧数字字号放大到 72px
- 底部进度条改为从左到右填充动画，时长 1.2s
```

**❌ 错误的反馈方式**：
```
- 感觉不太对（→ 哪里不对？）
- 再好看一点（→ 具体改什么？）
- 动画太快了（→ 改到多少秒？）
```

**反馈检查清单**：

| 维度 | 检查项 |
|------|--------|
| 颜色 | 色值是否匹配？对比度是否足够？ |
| 布局 | 间距、对齐、比例是否正确？ |
| 文字 | 字号、字重、行高是否合适？ |
| 动画 | 时序、缓动函数、持续时间是否自然？ |
| 整体 | 情绪基调是否与预览图一致？ |

### Step 5：录制交付（Record & Deliver）

所有场景在浏览器中跑通后，录屏交付：

**录制工具选择**：
| 工具 | 平台 | 特点 |
|------|------|------|
| FocuSee | Mac/Win | 自动缩放、鼠标高亮 |
| OBS Studio | 全平台 | 免费、可定制 |
| 系统录屏 | Mac (Cmd+Shift+5) | 零配置 |
| ScreenFlow | Mac | 专业级 |

**录制设置**：
- 分辨率：1920×1080
- 帧率：60fps（动画流畅）
- 格式：MP4 (H.264)
- 逐场景录制，后期可用简单工具拼接

**最终交付**：
- 不需要 After Effects / Premiere
- 如需拼接多场景，用 iMovie / CapCut 等轻量工具即可
- 重点在代码动画本身的质量，不在后期特效

---

## 技术栈推荐

### 轻量方案（推荐起步）

```
HTML + CSS Animations + Vanilla JS
```
- 零依赖，单文件即可运行
- 适合简单场景、快速迭代

### 中量方案

```
React + Tailwind + Framer Motion
```
- 组件化管理多场景
- Framer Motion 处理复杂动画
- 适合 3-5 个场景的视频

### 专业方案

```
Remotion（React 视频框架）
```
- 代码即视频，直接渲染 MP4
- 精确帧控制
- 适合批量生产、模板化视频
- 可配合 `remotion-*` 系列 Skill 使用

---

## 与其他 Skill 的协作

```
vsl-storyboard-writer  →  提供脚本分镜（Step 1）
         ↓
codex-video-workflow   →  视觉预览 + 代码复刻（Step 2-5）
         ↓
frontend-slides        →  如果是演示文稿形式的视频
huashu-design          →  如果需要高保真原型动画
remotion-*             →  如果选择 Remotion 技术栈
```

---

## 反模式（Anti-Patterns）

| ❌ 反模式 | ✅ 正确做法 |
|----------|-----------|
| 直接让 AI 生成视频 | 先用图片确认视觉，再用代码复刻 |
| 在图片层放关键文字 | 所有文字必须用代码渲染 |
| 一次性写完所有场景代码 | 逐场景实现，确认后再下一个 |
| 用模糊语言反馈修改 | 给出具体色值、像素值、秒数 |
| 追求后期特效 | 把精力放在代码动画本身的质量上 |
| 跳过视觉预览直接写代码 | 预览图是「对齐预期」的关键步骤 |

---

## 质量检查清单

在交付前逐项确认：

**视觉质量**：
- [ ] 每个场景的色彩与预览图一致
- [ ] 文字清晰可读，字号合适
- [ ] 布局比例在 16:9 下自然
- [ ] 暗色模式下对比度足够

**动画质量**：
- [ ] 动画节奏自然，不突兀
- [ ] 进场 / 退场有合理的缓动
- [ ] 元素出现顺序符合叙事逻辑
- [ ] 无卡顿、闪烁

**内容准确性**：
- [ ] 所有数据 / 数字正确
- [ ] 品牌名称 / Logo 正确
- [ ] 无拼写错误

**技术健壮性**：
- [ ] 浏览器可独立运行（无依赖缺失）
- [ ] 不同浏览器兼容
- [ ] 录制后视频无黑边

---

## 快速启动模板

如果用户说「做个产品视频」，按以下流程启动：

```
1. 确认视频目的和目标受众
2. 确认场景数量（建议 3-5 个）
3. 逐场景执行 Step 1-4
4. 全部场景通过后执行 Step 5
5. 交付最终视频文件
```

**预计耗时**：
- 3 场景简单视频：1-2 小时
- 5 场景中等复杂度：3-4 小时
- 10+ 场景专业视频：1 天
