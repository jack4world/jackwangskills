# 仓库约定

这是一个 Agent Skills 仓库，改编自 [mattpocock/skills](https://github.com/mattpocock/skills)。目标读者是**编程新手**，所有技能都必须服务于「边开发边学习」。

## 结构

```
skills/<skill-name>/
├── SKILL.md              必需，带 YAML frontmatter
├── agents/openai.yaml    必需，Codex 的 UI 元数据
└── <其他>.md             可选，该技能自己的参考文档
```

技能目录是扁平的，没有分桶。每个技能都必须同时出现在：

- `.claude-plugin/plugin.json` 的 `skills` 数组
- `README.md` 的技能一览表（技能名链到它的 `SKILL.md`）
- `skills/learn-start/SKILL.md` 的路由表和技能一览表

新增、改名、删除技能时三处都要同步。**一个不提新技能、或者还路由到已删技能的入口，是一个会说谎的路由。**

## 写技能的规矩

这套技能的读者是新手，所以每个 `SKILL.md` 都要落实这三条，并在必要时明说给用户听：

1. **能让用户动手的地方绝不代劳。** AI 搭台子（环境、骨架、测试、签名、import），把最值钱的那几行留空给用户。留空处统一用 `// 💡 请在这里填入你的代码`。
2. **术语当场翻译。** 任何黑话第一次出现就配一句白话解释，不要等用户问。讲不清的调用 Skill 工具 "jargon-buster"。
3. **一次只推进一件事。** 一个问题、一个任务、一个测试、一条建议。新手的挫败感几乎都来自一次给太多。

其他约定：

- **技能之间的依赖写成「调用 Skill 工具 "<name>"」**，不要写 `/skill` 也不要跨目录引用 `../other-skill/FILE.md`。共享的参考文档放在拥有它的技能目录里，别的技能通过调用该技能来用。
- **给用户看的输出格式要写成代码块模板**，不要只用散文描述。模板是给 agent 照抄的，散文会被自由发挥。
- **散文里不用破折号。** 该用逗号、冒号、句号、括号或连词的地方就用它们，不要做无脑字符替换。
- **frontmatter 的 `description` 同时写中英文触发词。** 中文写给用户看，英文触发短语（`Use when the user…`）提高模型自动命中率。

## 改完之后

```bash
claude plugin validate . --strict
```

版本号在 `.claude-plugin/plugin.json` 里手动维护。
