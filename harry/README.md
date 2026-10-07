# Harry 个人学习工作区 (Pi Study Workspace)

本项目为开源项目 [Pi (Earendil Works)](https://github.com/earendil-works/pi) 的个人专属学习与研究工作区。

---

## 1. 基础信息

- **工作区维护者**：Harry (Hz-186 / Harry-Hz-Zhang)
- **基准分支**：`harry`
- **Origin 远程**：`https://github.com/Harry-Hz-Zhang/pi.git` (个人 Fork)
- **Upstream 远程**：`https://github.com/earendil-works/pi.git` (原始上游仓库，仅同步，严禁推送)
- **工作区定位**：用于系统性理解 Pi 的核心架构、Agent 循环、多模型 Provider 调度、TUI 终端交互及扩展系统。所有探究文档、学习笔记和工具输出均统一收敛于 `harry/` 目录中。

---

## 2. 目录导航

```
harry/
├── README.md               # 本说明文档：工作区概况与使用指南
├── CODEGRAPH.md            # 代码图谱：Monorepo 架构、核心包职责、关键类与符号锚点
├── AGENTS.md               # 学习版 Agent 规范：指令指引、研读规范、探究模式与测试纪律
├── CLAUDE.md               # Claude Code 接入入口指引
├── UPSTREAM_AGENTS.md      # 上游项目原始 AGENTS.md 规范完整备份
└── .codegraph/             # 代码索引工具元数据隔离目录
```

---

## 3. 工作区约束与协作原则

1. **上游保护**：
   - 严禁从 `harry` 分支向上游 `upstream` 发起 PR 或推送。
   - 任何改动仅推送至 `origin harry`。
2. **源码非侵入**：
   - 源码研读以「理解架构与数据流」为主，优先编写外部学习测试（Study Tests）或最小可运行脚本，禁止在业务源码中大面积插入静态翻译注释，避免上游 `rebase` 产生密集冲突。
3. **符号与数据流导向**：
   - 架构分析与文档记录严格使用「文件路径 + 符号名（类名/函数名）」定位，禁止依赖易漂移的行号。
   - 记录关键节点时，标明真实的数据输入输出结构（JSON/TypeScript 格式样例）。
