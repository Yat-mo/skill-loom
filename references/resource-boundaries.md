# Resource Boundary Spec

## Keep in SKILL.md

- 触发条件
- 核心流程
- 必要的输出约束
- 复杂 Skill 的最小路由入口与关键坑点索引

## Move to references

- 长流程说明
- 示例集
- 评估标准
- 治理细则

## Move to scripts

- 可重复执行
- 需要确定性
- 适合自动化校验

## Move to evals

- should-trigger / should-not-trigger / near-neighbor 样例
- output eval 的 baseline、with-skill、assertions
- 防止用户已经指出过的失败再次发生

## Move to reports

- 运行脚本生成的验证结果
- `reports/skill-ir.json`
- 发布、评审、证据和缺失项说明

不要把报告里的生成结果反向塞回 `SKILL.md`，除非它已经变成稳定规则。

## 渐进结构

- `Single-file`：主题少于 3 个、没有重复流程，只保留 `SKILL.md`。
- `Folder-light`：出现 3–5 个主题或一个重复流程，按实际需要增加 `references/`、`scripts/` 或 `workflows/`。
- `Full`：存在多个独立任务路由、跨 harness 入口、反复出现的高代价坑点或长期维护责任，才增加路由清单、薄壳或 hooks。

行数只是评估信号，不是自动拆分命令。几个文件如果总是一起加载、一起修改，应优先合并。

## 记录边界

- 稳定约束写入规则或核心方法。
- 有序步骤写入 workflow。
- 高代价、非显然陷阱写入 gotcha/reference，并从相关任务路径激活。
- 会话记录、调试流水账、一次性叙事不要写进 Skill；使用 Git 历史或外部工作记录。

## 平台适配

平台中立语义保留在根 `SKILL.md` 与 references。只有目标平台需要时才生成适配器：

- OpenAI/Codex：`agents/openai.yaml`
- 通用跨 Agent 介面：`agents/interface.yaml`
- Cursor：`.cursor/skills/<name>/SKILL.md`
- 薄壳与 SessionStart hook：仅在目标 harness 支援且长会话/压缩风险已被证明时加入

## 根入口隔离

一个可安装 skill 包只能有一个可被递归发现的入口：根目录的 `SKILL.md`。

- 仓库内嵌示例使用 `SKILL.example.md`。
- 测试夹具使用 `SKILL.fixture.md`。
- 示例或夹具复制成独立 skill 后，再把入口重命名为 `SKILL.md`。
- 验证和打包时扫描整个源树与归档；如果根目录之外仍有精确命名的 `SKILL.md`，应当阻断发布。

原因不是目录整洁，而是安装器可能复制整个仓库，agent 又可能递归发现入口文件，从而把示例或夹具误激活成独立 skill。
