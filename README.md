# jackwangskills

面向零基础初学者的编程技能集。设计前提是**把事办成，同时让你看懂**：活全部由 AI 干完，但每个专业名词当场翻译成人话，每做一步都告诉你干了什么，遇到取舍给你选项由你拍板。

改编自 [Matt Pocock 的 skills](https://github.com/mattpocock/skills)（MIT）。原版是给熟练工程师用的强指令，这套把它改成了零基础也能全程跟得上的版本。

**这是我自己用的仓库**，公开只是为了方便跨机器安装。你要是路过觉得有用，随便拿。

## 固定分工

| 谁 | 干什么 |
| --- | --- |
| AI | 配环境、写测试、写代码、修报错、提交存档、翻译术语 |
| 你 | 两件事：**验收**（看一眼对不对）和**拍板**（有取舍时选一个） |

四条贯穿始终的原则：活 AI 干完选择留给你、术语当场翻译成人话、一次只推进一件事、**每跑一步跟一句解释**（不攒着汇报，不只贴命令输出）。

只有两类事必须你来：**只有你能做的**（注册账号、点授权、输密码、付钱）和**只有你能定的**（选哪个方案、要不要这么改）。第二类一律给 2 到 3 个选项，写清好处和代价，标出推荐哪个。

## 安装

### Claude Code（插件）

```bash
/plugin marketplace add jack4world/jackwangskills
/plugin install jackwangskills@jack4world
```

装完在任意项目里说一句「我是新手，不知道从哪开始」，`learn-start` 会自动接住并告诉你该敲哪个命令。

### Codex / Cursor / Trae 等（skills.sh）

```bash
npx skills@latest add jack4world/jackwangskills
```

会弹出一个可勾选的菜单，选技能、选要装到哪些 agent 上，文件会写进项目的 `.agents/skills/`。装出来的文件归你所有，可以直接改。

和插件方式二选一，同时装会让每个技能出现两遍。

## 技能一览

| 技能 | 怎么触发 | 什么时候用 | 你会得到 |
| --- | --- | --- | --- |
| [learn-start](./skills/learn-start/SKILL.md) | 自动 | 不知道该用哪个 | 判断你在哪一步，告诉你该敲哪个命令 |
| [jargon-buster](./skills/jargon-buster/SKILL.md) | 自动 | 有词听不懂 | 一句话白话加生活类比，外加一份[常见术语表](./skills/jargon-buster/glossary.md) |
| [wait-what](./skills/wait-what/SKILL.md) | 自动 | 整段话没跟上 | 先诊断卡在哪一层，再换一种讲法重讲，不是把原话说慢 |
| [mentor-grill](./skills/mentor-grill/SKILL.md) | `/jackwangskills:mentor-grill` | 想法还很模糊 | 一轮一问、每问带选项的需求澄清，最后落一份需求共识 |
| [learn-roadmap](./skills/learn-roadmap/SKILL.md) | `/jackwangskills:learn-roadmap` | 需求清楚，不知道先做哪个 | 一份每步做完都能看见成果的白话路线图 |
| [learn-tdd](./skills/learn-tdd/SKILL.md) | `/jackwangskills:learn-tdd` | 要做一个功能 | 先写测试说清要做成什么样，再把它做出来跑绿给你验收 |
| [learn-refactor](./skills/learn-refactor/SKILL.md) | `/jackwangskills:learn-refactor` | 代码写完想改好 | 一次只指一条坏味道，讲透原理，你点头我就改 |
| [learn-debug](./skills/learn-debug/SKILL.md) | `/jackwangskills:learn-debug` | 报错、白屏、跑不起来 | 报错翻译成人话，先建重现再猜原因，外加[十种常见报错速查](./skills/learn-debug/common-errors.md) |
| [learn-ship](./skills/learn-ship/SKILL.md) | `/jackwangskills:learn-ship` | 一步做完了要收尾 | 跑全量测试、替你 git commit 存档并讲清每条命令、勾掉路线图 |

六个技能**故意设成手动触发**：它们会接管整个流程，说一句「帮我优化这段代码」不该变成一整套流程。要走完整流程的时候才敲命令。

命令带 `jackwangskills:` 前缀，这是插件安装技能的固定形式（`<插件名>:<技能名>`）。嫌长可以只敲 `/learn` 让补全接手。

三个自动触发的不用敲命令，直接说人话就行：不知道从哪开始（`learn-start`）、有词不懂（`jargon-buster`）、**整段没跟上就说「没听懂」**（`wait-what`）。

分界标准是**接住的自动，接管的手动**：前三个只是接住你、换个说法，说完你手上的事还在原处；六个技能会接管整个流程，所以要你主动开。

## 典型流程

```
「我想做个记账的小工具」
        │  learn-start 自动接住，告诉你敲下面第一条
        ▼
/jackwangskills:mentor-grill      一轮一问，问清楚做给谁、存哪儿
        ▼   产出 .learn/需求共识.md
/jackwangskills:learn-roadmap     竖着切成 5 步，每步都能演示
        ▼   产出 .learn/路线图.md
/jackwangskills:learn-tdd         我写测试再写实现，红 → 绿 → 你验收
        │        └─ 卡在报错上： /jackwangskills:learn-debug
        ▼
/jackwangskills:learn-refactor    一次一条，把它改好
        ▼
/jackwangskills:learn-ship        全量测试 → 提交 → 勾掉这一步
        ▼
     下一步 ↺
```

任何一步卡在术语上，随时问「XX 是什么意思」，jargon-buster 会接住。

## 和原版的对应关系

| 原版技能 | 本仓库 | 改了什么 |
| --- | --- | --- |
| `grilling` / `grill-me` | `mentor-grill` | 原版一轮问一整批问题，改成每轮只问 1 个，每问必带 2-3 个选项、推荐项和「帮我选 A」的安全垫 |
| `tdd` | `learn-tdd` | 原版假设你会配环境、会写测试。改成 AI 全包环境、测试和实现，先看红再看绿，每一行核心代码都翻译成人话，最后指一个具体地方让你亲眼验收 |
| `to-tickets` | `learn-roadmap` | 保留「竖着切」的内核，但用夹心蛋糕的比方讲清楚为什么，任务标题一律白话，并解释每一步为什么排在这个位置 |
| `improve-codebase-architecture` | `learn-refactor` | 原版基于深模块理论扫全库出 HTML 报告。改成只看刚写的代码，一次只指一条具体坏味道，五段式讲清楚位置、问题、为什么、改完的样子、背后的原则 |
| `diagnosing-bugs` | `learn-debug` | 原版是 6 阶段硬纪律（最小化重现、可证伪假设、探针）。只保留最核心的一条（**没有稳定重现不许开始猜**），每个猜测都要带一句可验证的预测，修完必做复盘告诉你这是什么毛病 |
| `implement` | `learn-ship` | 原版 4 行，串起 TDD、全量测试、code-review、提交。这一版把重点压在**替你把代码存进档**上，顺手把三条 git 命令翻译一遍，代码没提交是会真丢的 |
| `wait-what` | `wait-what` | 原版 3 行（「重讲，用简单英语，用 CONTEXT.md 的词汇」）。教学版补上**先诊断卡在哪一层**（词不懂／不知道为什么／一次给太多／步子太大）、第二次必须换完全不同的形式、第三次讲不通就明确跳过，以及收尾让用户复述来验证 |
| （新增） | `jargon-buster` | 术语翻译，被其他技能随时调用 |
| （新增） | `learn-start` | 新手入口路由 |

**没有转的 18 个**，按对自用小项目的实际意义分三档：

- **不是给用户用的功能**：`ask-matt`（路由，本仓库是 `learn-start`）、`setup-matt-pocock-skills`、`writing-for-agents`
- **需要 issue tracker 或团队**：`triage`、`wayfinder`、`to-spec`、`to-questionnaire`、`handoff`。其中 `to-spec` 的位置已被 `mentor-grill` 产出的 `.learn/需求共识.md` 顶掉
- **以后可能会补**：`wizard`（第一次部署上线时会撞上）、`code-review`（`implement` 链条里目前缺的一环）、`research`、`prototype`、`resolving-merge-conflicts`、`domain-modeling`、`codebase-design`、`grill-with-docs`、`teach`

`teach` 和本仓库是两条路：它生成 HTML 课件、跨会话教一个**主题**；本仓库是**在做真项目的过程中**教。想系统学某门语言本身，用 `teach` 更合适。

## 本地开发

改完技能之后验证插件清单：

```bash
claude plugin validate . --strict
```

本地试装（不用先发到 GitHub）：

```bash
/plugin marketplace add /Users/daboluo/Project/codeskills
/plugin install jackwangskills@jack4world
```

仓库约定见 [AGENTS.md](./AGENTS.md)。

## License

MIT。原作版权归 Matt Pocock，改编部分版权归本仓库作者，详见 [LICENSE](./LICENSE)。
