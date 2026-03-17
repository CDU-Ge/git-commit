---
name: git-commit
description: 将用户的变更自动拆分为多个原子性提交，并使用约定式提交规范。
disable-model-invocation: true
---

# git-commit

你的任务是将用户的变更自动拆分为多个原子性提交，并使用约定式提交规范。每次提交必须指定要提交的文件路径，确保每个提交只包含一个逻辑变更。你需要根据文件类型自动分组，并生成清晰、简洁的提交消息。

不要询问用户是否要拆分提交，直接根据变更内容进行拆分。不要对文件的内容进行修改，只负责生成提交消息和指定要提交的文件路径。

提交消息的语言默认为 `简体中文`.

## 核心原则

1. 原子性：每个 commit 只包含一个逻辑变更
2. 清晰：使用约定式提交规范
3. 粒度：拆分为小提交而非大提交
4. 显式：必须指定要提交的文件
5. 自动：用户要求提交时自动拆分，无需询问

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

## 提交规范

- 使用动词开头，现在时态（add not added）
- 首字母小写（除非专有名词）
- 结尾不要句号
- 不超过 50 字符

正确：feat(auth): add OAuth2 support错误：Feat(Auth): Added OAuth2 Support.

## 原子性提交

错误：git commit -m "feat: add auth and update tests and fix typo"

正确：

```bash
git commit auth.py -m "feat(auth): add OAuth2 login"
git commit tests/auth_test.py -m "test(auth): add login tests"
git commit README.md -m "docs(readme): fix typo"
```

### 分组规则

按文件类型自动分组：

- 测试文件：`tests/`, `test_*.py`, `*.test.ts`, `*.spec.js`
- 文档文件：`*.md`, `README`, `CHANGELOG`
- 配置文件：`*.json`, `*.yaml`, `.*rc`
- 锁文件：`*-lock.json`, `Cargo.lock`, `poetry.lock`
- 代码文件：按目录或模块分组

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
