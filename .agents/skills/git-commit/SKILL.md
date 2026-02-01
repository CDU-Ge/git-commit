---
name: git-commit
description: Git commit 指南和最佳实践
disable-model-invocation: true
---

# Git Commit Guidelines

每当完成一个功能或修复一个 bug 时，编写清晰且有意义的 git commit 信息是非常重要的。
对于变更，不仅仅要描述"做了什么"，还要解释"为什么这么做"。这有助于团队成员理解代码的历史和意图。

## 核心原则

1. **原子性提交**：每个 commit 只包含一个逻辑单元的变更，便于回滚和代码审查
2. **清晰的信息**：使用约定式提交规范，明确说明变更的类型和范围
3. **充分的粒度**：优先选择分成多个小提交，而不是一个大的提交
4. **必须指定文件**：提交时必须显式指定要提交的文件路径

## 提交格式

项目采用[约定式提交规范](./references/conventionalcommits.md)：

```bash
git commit <files> -m "<type>(<scope>): <subject>"
```

**注意**：提交时 `<files>` 不能为空，必须指定具体的文件路径。

### 类型（Type）

常用的提交类型：

| 类型 | 说明 | 示例 |
|------|------|------|
| `feat` | 新功能 | feat(auth): add OAuth2 login support |
| `fix` | 修复 bug | fix(api): handle null response correctly |
| `docs` | 文档变更 | docs(readme): update installation instructions |
| `style` | 代码格式（不影响逻辑） | style(components): fix indentation |
| `refactor` | 重构（不是新功能也不是修复） | refactor(utils): simplify date parsing |
| `perf` | 性能优化 | perf(db): add index to user table |
| `test` | 测试相关 | feat(auth): add login tests |
| `chore` | 构建/工具链变更 | chore(deps): update lodash to 4.17.21 |
| `ci` | CI 配置 | ci(github): add automated tests |
| `build` | 构建系统 | build(windows): fix compilation error |

### 范围（Scope）

范围用于标识提交影响的部分，例如：

- 模块名：`auth`, `database`, `api`
- 文件类型：`config`, `middleware`
- 组件：`button`, `header`

### 破坏性变更

使用 `!` 或 `BREAKING CHANGE` 标记：

```bash
# 方式1: 使用 !
git commit -m "feat(api)!: remove deprecated endpoint"

# 方式2: 使用 BREAKING CHANGE
git commit -m "feat(api): remove deprecated endpoint

BREAKING CHANGE: The /api/v1/users endpoint is no longer supported"
```

## 提交最佳实践

### 1. 原子性提交示例

**❌ 不好的做法** - 一个提交包含多个变更：
```bash
git commit -m "feat: add user authentication and update tests and fix typo"
```

**✅ 好的做法** - 拆分为多个独立提交：
```bash
git commit auth.py -m "feat(auth): add OAuth2 login"
git commit tests/auth_test.py -m "test(auth): add login tests"
git commit README.md -m "docs(readme): correct typo in installation"
```

### 2. 提交粒度

遵循以下原则：

- 一个提交只做一件事
- 如果修改了多个不相关的文件，考虑拆分
- 测试代码与实现代码可以分开提交（如果测试是后续补充的）
- 文档更新与功能实现可以分开提交

### 3. 提交信息规范

- **描述（subject）**：使用动词开头，使用现在时态（"add" 而不是 "added"）
- **首字母小写**：除非是专有名词
- **结尾不要句号**：保持简洁
- **限制长度**：建议不超过 50 个字符

**示例**：

```text
✅ feat(auth): add OAuth2 support
✅ fix(api): handle timeout errors
❌ Feat(Auth): Added OAuth2 Support.
❌ fixing stuff
```

### 4. 提交正文和脚注

对于复杂的变更，可以添加正文和脚注：

```bash
git commit -m "fix(database): optimize query performance

- Add index on user_id column
- Refactor join operation to reduce N+1 queries
- Cache frequently accessed data

Performance impact: Query time reduced from 200ms to 50ms

Refs: #123
Reviewed-by: @username"
```

## 常见场景

### 新增功能

```bash
git commit lib/user.py -m "feat(user): add profile update method"
```

### 修复 Bug

```bash
git commit lib/parser.py -m "fix(parser): handle empty input correctly"
```

### 重构代码

```bash
git commit lib/utils.py -m "refactor(utils): extract validation logic"
```

### 添加测试

```bash
git commit tests/test_utils.py -m "test(utils): add validation tests"
```

### 更新文档

```bash
git commit README.md -m "docs(readme): add usage examples"
```

### 修改配置

```bash
git commit .eslintrc.json -m "chore(config): enable no-unused-vars rule"
```

## 修改错误的提交

如果提交信息有错误：

```bash
# 修改最后一次提交信息
git commit --amend -m "corrected commit message"

# 修改已推送的提交（谨慎使用）
git commit --amend -m "corrected commit message"
git push --force-with-lease
```

## 工作流建议

1. **开发前**：拉取最新代码
2. **开发中**：频繁提交本地变更
3. **完成功能**：整理提交历史（rebase if needed）
4. **推送前**：检查提交信息格式
5. **创建 PR**：使用清晰的提交历史辅助代码审查

## 参考资源

- [约定式提交规范](./references/conventionalcommits.md) - 完整的规范说明
- [Conventional Changelog](https://github.com/conventional-changelog/conventional-changelog) - 自动生成 CHANGELOG
- [Commitlint](https://github.com/conventional-changelog/commitlint) - 提交信息 lint 工具
