---
name: git-commit
description: Git commit 指南和最佳实践
disable-model-invocation: true
---

# Git Commit 指南

## 核心原则

1. 原子性：每个 commit 只包含一个逻辑变更
2. 清晰：使用约定式提交规范
3. 粒度：拆分为小提交而非大提交
4. 显式：必须指定要提交的文件

## 提交格式

```bash
git commit <files> -m "<type>(<scope>): <subject>"
```

提交时必须指定具体文件路径。

## 类型

- feat: 新功能
- fix: 修复 bug
- docs: 文档变更
- style: 代码格式（不影响逻辑）
- refactor: 重构（不是新功能也不是修复）
- perf: 性能优化
- test: 测试相关
- chore: 构建/工具链变更
- ci: CI 配置
- build: 构建系统

## 范围

标识影响的部分，如模块名（auth、api、db）、文件类型（config、middleware）、组件名（button、header）。

## 破坏性变更

```bash
git commit -m "feat(api): remove deprecated endpoint

BREAKING CHANGE: /api/v1/users is no longer supported"
```

或使用 `!`：`feat(api)!: remove deprecated endpoint`

## 提交规范

- 使用动词开头，现在时态（add not added）
- 首字母小写（除非专有名词）
- 结尾不要句号
- 不超过 50 字符

正确：feat(auth): add OAuth2 support
错误：Feat(Auth): Added OAuth2 Support.

## 原子性提交

错误：git commit -m "feat: add auth and update tests and fix typo"

正确：
```bash
git commit auth.py -m "feat(auth): add OAuth2 login"
git commit tests/auth_test.py -m "test(auth): add login tests"
git commit README.md -m "docs(readme): fix typo"
```

## 常见场景

```bash
# 新功能
git commit lib/user.py -m "feat(user): add profile update method"

# 修复 bug
git commit lib/parser.py -m "fix(parser): handle empty input"

# 重构
git commit lib/utils.py -m "refactor(utils): extract validation logic"

# 添加测试
git commit tests/test_utils.py -m "test(utils): add validation tests"

# 更新文档
git commit README.md -m "docs(readme): add usage examples"

# 修改配置
git commit .eslintrc.json -m "chore(config): enable no-unused-vars"
```

## 修改提交

```bash
git commit --amend -m "corrected message"
git push --force-with-lease  # 已推送时使用
```
