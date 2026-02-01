---
name: git-commit
description: git commit 指南
disable-model-invocation: true
---

# Git Commit Guidelines

每当完成一个功能或修复一个 bug 时，编写清晰且有意义的 git commit 信息是非常重要的。
对于变更，不仅仅要描述“做了什么”，还要解释“为什么这么做”。这有助于团队成员理解代码的历史和意图。
当有大量变更时，建议将其拆分为多个小的 commit，每个 commit 只包含一个逻辑单元的变更。 这样可以更容易地回滚和审查代码。

## Guidelines

- 项目参用[约定式提交规范](./references/conventionalcommits.md)来编写 commit 信息。
- 提交时必须包含目标文件: `git commit <files> -m "<type>(<scope>): <subject>"`。
- 当遇到提交时是分成小模块提交，还是合并成一个大提交时，请优先选择分成小模块提交。

## 提交命令

```bash
git commit -m "<type>(<scope>): <subject>" <files>
```

注意: 提交时，`<files>` 不能为空，必须指定具体的文件路径。
