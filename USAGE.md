# 使用指南：把手册接入自己的项目

本仓库是工程方法和文件模板库。配套 npm 工具是独立仓库 [vibe-workspace-kit](https://github.com/mxpsept/vibe-workspace-kit)，可运行 `npm install --global vibe-workspace-kit` 安装（需要 Node.js 20+ 和 Git），然后使用 `vibe --help` 查看命令。安装与 Feature 快速入门见 [README](README.md#如何使用)，完整流程见 [工具工作流文档](https://github.com/mxpsept/vibe-workspace-kit/blob/main/docs/v0.2-workflow.md)。

下面介绍不安装 CLI、直接复制模板的接入方式。只阅读时无需 Node.js；执行下面的复制步骤需要 Git 和 Bash。业务项目的运行环境由业务项目自己决定。

## 1. 获取手册

```bash
git clone https://github.com/mxpsept/vibe-coding-handbook.git
cd vibe-coding-handbook
```

已经获取仓库的读者可直接使用当前目录。先阅读 [场景入口](START-HERE.md)，按任务选择资料，无需把整本手册放进 Agent 上下文。

| 文件类型 | 实际用法 |
| --- | --- |
| `handbook/` | 阅读相关章节，确定工作流程和决策边界 |
| `templates/` | 复制到业务仓库，填写为项目自己的事实和规范 |
| `prompts/` | 复制相关提示词到 Agent 会话，提供实际文件路径和当前目标 |
| `checklists/` | 实施或交付前逐项检查，记录未满足项 |
| `examples/flowops/` | 参考产物写法；FlowOps 是虚构案例，不代表你的业务规则 |
| `starter-kits/` | 按场景选用的模板组合，不是可运行应用 |

## 2. 已有项目：复制最小文件集

以下命令在手册仓库根目录执行。把 `project_dir` 改为你自己的业务项目绝对路径；示例采用 Bash，`cp -i` 会在目标文件存在时询问是否覆盖。

```bash
handbook_dir="$PWD"
project_dir="/absolute/path/to/your-project"

# 先确认路径正确且项目已存在，再继续执行后续命令。
cd "$project_dir" || exit 1
mkdir -p docs/architecture docs/features/FEAT-001
cp -i "$handbook_dir/starter-kits/codex/AGENTS.example.md" AGENTS.md
cp -i "$handbook_dir/starter-kits/enterprise-project/architecture-context.example.md" docs/architecture/architecture-context.md
cp -i "$handbook_dir/templates/requirements/requirement-spec.template.md" docs/features/FEAT-001/feature-spec.md
cp -i "$handbook_dir/starter-kits/codex/implementation-packet.example.md" docs/features/FEAT-001/implementation-packet.md
cp -i "$handbook_dir/starter-kits/codex/verification-report.example.md" docs/features/FEAT-001/verification.md
```

如果业务仓库已有 `AGENTS.md`，保留原文件，手工合并适用规则。这里的 `FEAT-001` 是示例任务编号，可按项目约定更名，并同步更新文件内引用。

复制后必须修改以下内容：

- `AGENTS.md`：填写仓库目录、真实的安装/测试/构建命令、架构边界、停止条件和 Git 权限。可参照更通用的 [Agent 规则模板](templates/agent/AGENTS.example.md) 补充；不要保留 `...` 占位符。
- `architecture-context.md`：替换示例技术栈与模块划分，记录现有系统事实。
- `feature-spec.md`：填写本次需求、业务规则、范围、非目标和可验证的验收标准。
- `implementation-packet.md`：替换 FlowOps 的逾期任务示例，引用本项目规范，明确允许修改的模块、禁止扩展的范围和停止条件。
- `verification.md`：删除示例测试名和 PASS 结果，等实际执行验证后再记录命令、证据和未验证项。

`AGENTS.md` 放稳定的仓库规则，具体需求放任务目录。不要把整本手册、聊天历史或密钥复制进规则文件。

## 3. 让 Agent 完成第一个任务

在 Coding Agent 中打开业务项目，发送下面的提示词。若使用其他工具，也可以显式提供这些文件作为上下文；本仓库不包含自动生成各工具规则文件的适配器。

```text
请先读取：
- AGENTS.md
- docs/architecture/architecture-context.md
- docs/features/FEAT-001/feature-spec.md
- docs/features/FEAT-001/implementation-packet.md

本轮先不要修改代码。检查相关实现与测试，报告：
1. 需求对应的模块、可复用实现及现有约定；
2. 实际可执行的验证命令；
3. 规范冲突、缺失业务规则或 SPEC_GAP；
4. 最小实施计划、非目标和停止条件。
不要自行补充权限、状态流转或时间边界规则。
```

先解决阻断性未知项并确认关键规则，再发送：

```text
按已确认的实施计划完成 FEAT-001，遵守 AGENTS.md 和任务包。
运行项目实际支持的测试、构建和检查命令。
将每条验收标准对应的证据、实际执行命令与结果写入
 docs/features/FEAT-001/verification.md。
未执行或失败的检查必须明确标注；遇到停止条件时报告受阻部分。
本次不提交、不推送、不发布。
```

完成后，对照需求和代码差异进行审查，使用 [Agent 交接检查表](checklists/implementation/agent-handoff.md)。完整的分阶段提示词见 [Feature Session Prompt Pack](prompts/implementation/codex-feature-session.md)。

第一次实践的完成标准是：任务范围明确、代码符合已确认规则、每条验收标准有证据、未验证项已列明。复制完模板不等于完成接入。

## 4. 新项目：先澄清，再交给 Agent 实施

没有现成代码时，先使用 [Enterprise Project Bootstrap Kit](starter-kits/enterprise-project/README.md) 和 [Bootstrap 检查表](starter-kits/enterprise-project/BOOTSTRAP-CHECKLIST.md)。

1. 参照 [Product Brief 示例](starter-kits/enterprise-project/product-brief.example.md)，写明用户、问题、目标和非目标。
2. 将 [Project Bootstrap Session Prompt](prompts/discovery/project-bootstrap-session.md) 中的提示词发送给 Agent，并附上自己的想法与已知证据。
3. 澄清术语、关键流程、状态和权限规则，把事实、假设与未知项分开记录。
4. 参考 [Design Brief](starter-kits/enterprise-project/design-brief.example.md) 和 [Architecture Context](starter-kits/enterprise-project/architecture-context.example.md)，确认首个功能所需的设计与技术边界。
5. 选择一个有限的端到端功能，按本文第 2、3 步创建任务包、实施并验证。

需要查看完整产物时，阅读 [FlowOps 项目启动案例](examples/flowops/16-project-bootstrap/README.md)，把示例业务内容替换成自己的项目事实。

## 5. 常见问题

**应该执行哪个 npm / npx 命令？** 配套工具的安装命令是 `npm install --global vibe-workspace-kit`，安装后执行 `vibe --help`。仅复制本仓库模板时无需安装依赖。参考章节包含未来设计，实际可用命令以工具帮助和对应版本文档为准。

**Agent.md 在哪里？** 当前仓库提供的是 `templates/agent/AGENTS.example.md` 和 `starter-kits/codex/AGENTS.example.md` 两份示例，没有根目录的 `Agent.md` 或 `AGENTS.md`。接入时将选用的示例修改为业务仓库根目录的 `AGENTS.md`。

**模板里的命令和测试结果可以直接用吗？** 不可以。命令、测试名、路径和 FlowOps 业务规则都是待适配内容；验证报告中的示例结果也不是你项目的执行证据。

**需求发生变化怎么办？** 先更新需求、规则和任务包，再让 Agent 修改代码。已有系统的变化可使用 [Brownfield Change Packet](templates/implementation/brownfield-change-packet.template.md)，不要仅在会话里追加口头需求。
