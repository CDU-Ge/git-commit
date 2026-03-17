# Git Commit 类型说明

## feat: 新功能

添加新功能或特性。

示例：feat(auth): add OAuth2 authentication support
示例：feat(api): add user profile endpoint

## fix: Bug 修复

修复代码中的错误或缺陷。

示例：fix(auth): handle token expiration correctly
示例：fix(api): prevent null pointer exception in user lookup

## docs: 文档变更

修改、添加或删除文档。

示例：docs(readme): update installation instructions
示例：docs(api): add authentication documentation

## style: 代码格式

修改代码格式，不影响逻辑。

示例：style(components): fix indentation in Button
示例：style(utils): convert tabs to spaces

## refactor: 重构

重构代码，不改变功能行为。

示例：refactor(auth): extract validation to separate module
示例：refactor(utils): rename parseDate to parseDateTime

## perf: 性能优化

提升代码性能。

示例：perf(api): add Redis caching for user data
示例：perf(db): add composite index on user_id and created_at

## test: 测试相关

添加、修改或删除测试。

示例：test(auth): add tests for login validation
示例：test(api): add integration tests for user endpoint

## chore: 杂项

不修改源代码或测试的变更。

示例：chore(deps): update lodash to 4.17.21
示例：chore(config): add TypeScript configuration

## build: 构建系统

修改构建系统或外部依赖。

示例：build(webpack): upgrade to version 5
示例：build(scripts): add production build optimization

## ci: CI 配置

修改 CI 配置文件和脚本。

示例：ci(github): add automated testing workflow
示例：ci(jenkins): update deployment pipeline

## 类型选择

是否修改代码逻辑？
- 否：docs（文档）或 style（格式）
- 是，修复 bug：fix
- 是，添加新功能：feat
- 是，改善性能：perf
- 是，重构代码：refactor
- 是，修改测试：test
- 否：chore / build / ci

## 破坏性变更

```bash
# 方式 1: 添加 !
feat(api)!: remove deprecated user endpoint

# 方式 2: 脚注说明
feat(api): remove deprecated user endpoint

BREAKING CHANGE: /api/v1/users is removed. Use /api/v2/users instead.
```

## 范围（Scope）选择

按模块：auth、api、db、ui、utils
按层次：controller、service、model、view
按功能：user、payment、notification

使用简短名词，保持团队一致性。
