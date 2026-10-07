# Harry 工作区 Agent 协作与学习规范 (AGENTS.md)

本文件是针对 Harry 个人学习工作区的 Agent 交互与代码研读规范。

---

## 1. 核心定位与参考索引

- **代码图谱索引**：在进行代码修改、重构或逻辑分析前，必须首先查阅 [harry/CODEGRAPH.md](file:///Users/zhanghongze/PycharmProjects/pi/harry/CODEGRAPH.md)。
- **工作区概览**：查阅 [harry/README.md](file:///Users/zhanghongze/PycharmProjects/pi/harry/README.md)。
- **上游原始规范**：完整继承并参照上游项目约束 [harry/UPSTREAM_AGENTS.md](file:///Users/zhanghongze/PycharmProjects/pi/harry/UPSTREAM_AGENTS.md)。

---

## 2. 交互风格与输出规范

- **回复语言**：默认使用中文回答。代码符号、命令、日志保持原始语言。
- **技术文风**：直接、客观、紧凑，禁止情绪化修饰词。
- **先论后据**：先给出直接结论，再展示推导链路与验证过程。
- **符号定位**：禁止引用代码物理行号，一律使用「文件路径 + 函数名/类名/类型名」作为稳定坐标。
- **数据结构示例**：解释复杂流程时，必须给出具体的数据结构样例（`[]` 或 `{}`）。

---

## 3. Git 操作与仓库纪律

- **当前分支**：所有学习与改动必须在 `harry` 分支上进行。
- **远程推送约束**：
  - `origin` (`https://github.com/Harry-Hz-Zhang/pi.git`)：允许提交与推送。
  - `upstream` (`https://github.com/earendil-works/pi.git`)：**绝对严禁推送**，仅作为上游更新同步源。
- **提交范围控制**：
  - 严禁 `git add .` 或 `git add -A`。
  - 必须显式暂存具体修改的文件：`git add path/to/file`。
  - 提交信息格式：`docs: <简要描述>` 或 `test: <简要描述>`，保持简练明确。

---

## 4. 项目命令与校验规范

- **代码改动后校验**：
  ```bash
  npm run check
  ```
  该命令会运行 Biome 格式化检查、依赖锁定校验、TypeScript 类型检查（`tsc --noEmit`）以及浏览器冒烟检查。在提交代码前确保无错误。
- **单元测试执行**：
  - 严禁直接无参运行 vitest（会触发需要真实 Token 的 e2e 测试）。
  - 本地非 e2e 测试使用根目录脚本：
    ```bash
    ./test.sh
    ```
  - 指定文件单测：
    - Vitest 包：
      ```bash
      node "$(git rev-parse --show-toplevel)/node_modules/vitest/dist/cli.js" --run test/specific.test.ts
      ```
    - TUI 包 (`node:test`)：
      ```bash
      node --test test/specific.test.ts
      ```

---

## 5. 源码研读与动态探究规范

1. **避免源码侵入式注水**：
   - 不要在业务逻辑中大面积插入静态翻译注释，防止上游 `rebase` / `merge` 时产生灾难级文本冲突。
2. **测试驱动探究 (Study Tests)**：
   - 探究核心逻辑时，优先编写最小可运行用例或在相关测试目录中编写学习单测验证猜想。
3. **临时探究脚本**：
   - 如需编写临时验证脚本，写入系统 `/tmp` 目录或 `harry/scratch/` 中执行，测试完成后按需沉淀或清理。

---

## 6. 知识性文档编写与子代理多轮核验规范

在本项目中编写任何需要的知识性文档时，必须遵循以下标准并由主 Agent 开启子 Agent 进行一轮一轮的严格验证：

1. **必须保证文档当中的所有话都是人话，没有黑化的成分**：行文通俗自然，禁止怪异偏激或晦涩难懂的表达。
2. **所有的话人类都是可以正常阅读的，没有 AI 的味道**：坚决剔除任何机械感、公进化套话、罐头式过渡句、空洞宏大的排比句，以纯正的人类工程师口吻书写。
3. **不要用专业的知识解释专业的知识**：严禁循环定义与术语套娃。涉及专业概念时，必须结合真实流程、具体输入输出或通俗类比解释清楚。

**对应对照与修复纪律（着重强调）**：
- 子 Agent 必须保证所有的内容没有逻辑错误以及表述上的不清晰，必须和原本的代码一条一条进行对应对照（核验文件路径、函数名、类名及其实际逻辑）。
- 如果审查中出现上述任何问题，主 Agent **必须开启新的子 Agent 进行修复**（着重强调：绝对不要复用原有的子 Agent）。修复后再次派验证子 Agent 复核，直至完全合格。

