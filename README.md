# Codex Video Workflow

用 AI 图片生成做视觉预览 + 代码精确复刻动画，绕过传统剪辑软件（Premiere / After Effects），直接产出专业产品视频。

## 这是什么？

**Codex Video Workflow** 是一种「双层分离」的视频制作方法：

- **Image Layer（图片层）**：用 GPT-Image-2 等 AI 图片生成工具，快速出视觉参考图，对齐预期
- **Code Layer（代码层）**：用 Codex / Claude 精确复刻动画，确保文字、数据、布局像素级准确

两层叠加 = 既有设计感，又有精确控制。

> 灵感来源：[@Formulasearch](https://x.com/Formulasearch/status/2051491008378974303)

## 适用场景

| 场景 | 说明 |
|------|------|
| 🖥 产品功能演示 | Dashboard、数据面板、SaaS walkthrough |
| 📚 教学/教程视频 | 步骤展示、操作流程可视化 |
| 📱 社交媒体短视频 | 产品亮点、功能发布 |
| 💼 销售/营销素材 | 客户 pitch、方案展示 |

## 工作流一览

```
Step 1: 脚本分镜 → 定义布局、情绪、文字、动画序列
Step 2: 视觉预览 → AI 生成 16:9 参考图，确认视觉方向
Step 3: 代码复刻 → 交给 Codex/Claude 精确实现
Step 4: 迭代调优 → 用具体指标反馈修改（色值、像素、秒数）
Step 5: 录制交付 → 浏览器录屏，轻量拼接即可
```

## 核心原则

1. **文字/数据/布局 → 必须用代码实现**（不依赖 AI 生成图片中的文字）
2. **纹理/插画/氛围 → 可以用 AI 图片生成**
3. **逐场景迭代**，确认一个再做下一个
4. **用具体指标反馈**，不要模糊描述

## 技术栈选择

| 方案 | 技术栈 | 适合场景 |
|------|--------|---------|
| 轻量 | HTML + CSS Animations + Vanilla JS | 快速迭代、简单场景 |
| 中量 | React + Tailwind + Framer Motion | 3-5 场景的组件化视频 |
| 专业 | Remotion（React 视频框架） | 批量生产、模板化视频 |

## 使用方式

在 Claude Code / Codex 中直接说：

```
做个产品演示视频
```

或：

```
用 codex-video-workflow 方法，帮我做一个 Dashboard 功能介绍视频
```

Skill 会按五步工作流引导你完成整个过程。

## 预计耗时

| 规模 | 耗时 |
|------|------|
| 3 场景简单视频 | 1-2 小时 |
| 5 场景中等复杂度 | 3-4 小时 |
| 10+ 场景专业视频 | 1 天 |

## 与其他 Skill 的协作

- `vsl-storyboard-writer` → 提供脚本分镜
- `frontend-slides` → 演示文稿形式的视频
- `huashu-design` → 高保真原型动画
- `remotion-*` 系列 → Remotion 技术栈支持

## 文件结构

| 文件 | 用途 | 加载时机 |
|------|------|---------|
| `SKILL.md` | 核心工作流与方法论 | 始终加载 |
| `README.md` | 面向用户的说明文档 | 按需查阅 |

## Credits

方法论来源：[@Formulasearch](https://x.com/Formulasearch/status/2051491008378974303)

## License

MIT
