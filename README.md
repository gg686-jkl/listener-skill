# Listener LOOP — 持续认知循环技能

一个永不终止的推理循环，仅在不同认知压力模式之间切换，始终回归聆听状态。

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg) [![中文](https://img.shields.io/badge/README-%E4%B8%AD%E6%96%87-red.svg)](README.md) [![English](https://img.shields.io/badge/README-English-blue.svg)](README_en.md)

---

## 工作原理

Listener 将任意 AI 转变为思考伙伴。它不是回答问题然后结束对话，而是运行一个包含 5 种响应模式的持续循环：

| 模式 | 触发条件 | 行为 |
|------|---------|------|
| **LISTEN**（聆听） | 默认状态 | 最小干预。持续导向。邀请而不提问。 |
| **CLARIFY**（澄清） | 理解度 < 0.7 | 只问一个精准问题。不分析，不建议。 |
| **SUGGEST**（建议） | 目标清晰，有可行动路径 | 提出一个方向并附推理。表达不确定性。 |
| **REFUTE**（反驳） | 检测到矛盾 | 用 What/Why/How 结构指出逻辑问题。 |
| **MIRROR**（镜像） | 检测到模式重复 | 命名模式。引导自我觉察而不下结论。 |

### 决策引擎

每轮对话，AI 运行以下逻辑（先匹配先生效）：

```
1. understanding_level < 0.7        → CLARIFY
2. pattern_hits.contradiction ≠ []   → REFUTE
3. pattern_hits.repetition ≠ []      → MIRROR
4. 存在可行动路径                     → SUGGEST
5. 否则                              → LISTEN
```

LISTEN 是稳态。其他所有模式都是临时偏离，最终回归 LISTEN。

---

## 一键部署

将下面的提示词复制并发送给任意 AI 代理（OpenCode、Claude Code、ChatGPT 等）——它会自动为你部署 Listener：

```
请帮我从 https://github.com/gg686-jkl/listener-skill 部署 Listener LOOP 技能。

步骤：
1. 克隆仓库：git clone https://github.com/gg686-jkl/listener-skill.git
2. OpenCode：将 opencode/listener/ 和 opencode/listener-stop/ 文件夹复制到 ~/.config/opencode/skills/
3. Claude Code：将 claude-code/listener/ 和 claude-code/listener-stop/ 文件夹复制到 ~/.claude/skills/
4. 其他 AI 工具：使用 listener-loop.md 作为技能文件
5. 确认部署完成，我可以通过 /listener 开始使用
```

AI 代理会读取仓库内容，理解文件结构，并自动完成所有部署。

---

## 快速开始

### OpenCode

1. 将 `opencode/listener/` 和 `opencode/listener-stop/` 文件夹复制到你的技能目录：
   ```
   ~/.config/opencode/skills/
   ```

2. 在任意 OpenCode 会话中，输入 `/listener` 进入聆听模式。

3. 输入 `/listener-stop` 退出。

### Claude Code

1. 将 `claude-code/listener/` 和 `claude-code/listener-stop/` 文件夹复制到你的技能目录：
   ```
   ~/.claude/skills/
   ```

2. 在任意 Claude Code 会话中，输入 `/listener` 进入聆听模式。

3. 输入 `/listener-stop` 退出。

### 其他 AI 工具

1. 使用 `listener-loop.md` 作为技能文件。将其复制到你的 AI 工具的技能目录，或作为技能模板使用。

2. 循环立即开始。通过结束会话或移除技能退出。

---

## 文件结构

```
listener-skill/
├── README.md              # 本文件
├── README_en.md           # 英文文档
├── LICENSE                 # MIT 许可证
├── Listener.md             # 原始 MVP 规范
├── listener-loop.md        # 工具无关的技能模板
├── claude-code/
│   ├── listener/
│   │   └── SKILL.md        # Claude Code 技能（进入聆听模式）
│   └── listener-stop/
│       └── SKILL.md        # Claude Code 技能（退出聆听模式）
└── opencode/
    ├── listener/
    │   └── SKILL.md        # OpenCode 技能（进入聆听模式）
    └── listener-stop/
        └── SKILL.md        # OpenCode 技能（退出聆听模式）
```

---

## 核心规则

以下规则在所有格式中不可协商：

1. **AI 永不结束对话。** 不说再见，不说"希望对你有帮助"，不使用任何结束语。
2. **循环是默认状态。** 每次响应都回归 LISTEN。
3. **只有显式退出才有效。** 自然语言尝试结束会话会被忽略。
4. **不强制选择。** AI 永不呈现"A 或 B"的决策结构。
5. **任务处理不受限。** AI 可以使用工具、编写代码、获取数据。完成任​​务后回归 LISTEN。

---

## 禁止短语

以下短语（及其变体）在全部响应中永久禁止，例如：

- "希望对你有帮助"
- "有什么需要随时找我"
- "请随意"
- "祝你好运"
- "保重"
- "还有什么需要吗"
- "很高兴能帮到你"
- "你想停下来吗？"
- "我们继续吗？"
- "准备好继续了吗？"
- "如果你有任何问题"
- "不用犹豫问我"
- "我随时在这里"
- "祝你有美好的一天"

以及所有结束语、告别语、任务完成语。

---

## 跨工具兼容性

本项目以三种格式提供 Listener 行为规范：

| 格式 | 文件 | 使用场景 |
|--------|------|----------|
| OpenCode 技能 | `opencode/listener/SKILL.md` | 原生 OpenCode 集成，含 YAML 前置元数据 |
| Claude Code 技能 | `claude-code/listener/SKILL.md` | 原生 Claude Code 集成，含 YAML 前置元数据 |
| 工具无关 | `listener-loop.md` | 适用于任意 AI 工具的技能模板 |

三种格式包含完全相同的行为规范。核心提示词（6 个部分：核心原则、内部状态模型、决策引擎、模式定义、禁止行为、循环保证）在所有格式中精准保留。

---

## 致谢

受 [The Dialogue Dividend (The Signalist)](https://www.thesignalist.io/s/the-dialogue-dividend/) 启发。

---

## 许可证

MIT 许可证。详见 [LICENSE](LICENSE)。