# Git Commit 类型说明

本文档详细说明了各种 Git commit 类型的使用场景和最佳实践。

## 类型概览

### feat: 新功能

用于添加新的功能或特性。

**何时使用：**
- 添加新的用户功能
- 新增 API 接口
- 添加新的配置选项
- 实现新的业务逻辑

**示例：**
```bash
feat(auth): add OAuth2 authentication support
feat(api): add user profile endpoint
feat(ui): add dark mode toggle
feat(database): add migration for user preferences table
```

**注意事项：**
- 不应包含 bug 修复（如果有 bug，单独提交 fix）
- 不应包含重构（重构应该单独提交）
- 测试代码可以在同一个 feat 提交中

---

### fix: Bug 修复

用于修复代码中的错误、缺陷或问题。

**何时使用：**
- 修复导致程序崩溃的问题
- 修复计算错误
- 修复边界条件问题
- 修复内存泄漏
- 修复并发问题

**示例：**
```bash
fix(auth): handle token expiration correctly
fix(api): prevent null pointer exception in user lookup
fix(ui): resolve layout issue on mobile devices
fix(parser): handle escaped characters in JSON
```

**注意事项：**
- 明确说明修复了什么问题
- 如果可能，在提交正文中描述问题的原因
- 引用相关的 issue 编号

---

### docs: 文档变更

用于文档的修改、添加或删除。

**何时使用：**
- 更新 README
- 添加 API 文档
- 修改注释
- 更新使用说明
- 添加代码示例

**示例：**
```bash
docs(readme): update installation instructions
docs(api): add authentication documentation
docs(code): add JSDoc comments to utility functions
docs(guide): fix broken link in getting started guide
```

**注意事项：**
- 仅包含文档变更，不应包含代码逻辑修改
- 代码注释的修改通常使用 docs 类型

---

### style: 代码格式

用于修改代码格式，不影响代码逻辑。

**何时使用：**
- 调整缩进
- 修改空格或空行
- 统一分号使用
- 修改代码格式（如单引号 vs 双引号）

**示例：**
```bash
style(components): fix indentation in Button component
style(utils): convert tabs to spaces
style(api): add missing newlines at end of files
```

**注意事项：**
- 不应包含功能变更
- 不应包含逻辑修改
- 可以使用工具自动格式化后统一提交

---

### refactor: 重构

用于重构代码，不改变功能行为。

**何时使用：**
- 提取函数或方法
- 重命名变量或函数
- 改变代码结构
- 优化代码组织
- 简化复杂逻辑

**示例：**
```bash
refactor(auth): extract validation logic to separate module
refactor(utils): rename parseDate to parseDateTime
refactor(api): simplify error handling with middleware
refactor(db): replace raw queries with ORM methods
```

**注意事项：**
- 功能行为必须保持不变
- 如果同时优化了性能，考虑使用 perf 类型
- 如果修复了 bug，应该使用 fix 类型

---

### perf: 性能优化

用于提升代码性能。

**何时使用：**
- 优化算法
- 添加缓存
- 减少网络请求
- 优化数据库查询
- 减少内存使用

**示例：**
```bash
perf(api): add Redis caching for user data
perf(db): add composite index on user_id and created_at
perf(utils): replace O(n²) algorithm with O(n log n)
perf(images): lazy load images in gallery view
```

**注意事项：**
- 明确说明性能改进的效果
- 如果可能，在提交正文中包含性能数据

---

### test: 测试相关

用于添加、修改或删除测试。

**何时使用：**
- 添加单元测试
- 添加集成测试
- 修复测试代码
- 更新测试用例
- 重构测试代码

**示例：**
```bash
test(auth): add tests for login validation
test(api): add integration tests for user endpoint
test(utils): fix failing test for date parsing
test(e2e): add test for checkout flow
```

**注意事项：**
- 测试代码的修改应使用 test 类型
- 实现代码的同时添加测试，可以分开提交

---

### chore: 杂项

用于其他不修改源代码或测试文件的变更。

**何时使用：**
- 更新依赖包
- 修改构建配置
- 更新工具配置
- 添加或修改 .gitignore
- 更新开发工具

**示例：**
```bash
chore(deps): update lodash to version 4.17.21
chore(config): add TypeScript configuration
chore(gitignore): add .DS_Store to ignore list
chore(build): update webpack configuration
chore(tools): add prettier to project
```

**注意事项：**
- 不应包含功能代码的修改
- CI 配置的修改建议使用 ci 类型

---

### build: 构建系统

用于修改构建系统或外部依赖。

**何时使用：**
- 修改构建脚本
- 更新构建工具
- 修改 npm scripts
- 添加或删除依赖
- 修改 webpack/vite 配置

**示例：**
```bash
build(webpack): upgrade to version 5
build(scripts): add production build optimization
build(npm): add prepare script for pre-commit hooks
build(docker): update Dockerfile for multi-stage build
```

**注意事项：**
- 依赖版本的更新也可以使用 chore(deps)

---

### ci: CI 配置

用于修改 CI 配置文件和脚本。

**何时使用：**
- 修改 GitHub Actions 工作流
- 修改 Jenkins 配置
- 添加自动化测试
- 修改部署脚本

**示例：**
```bash
ci(github): add automated testing workflow
ci(jenkins): update deployment pipeline
ci(docker): add image build automation
ci(actions): configure notifications on failure
```

**注意事项：**
- 仅包含 CI/CD 配置的修改
- 不应包含应用代码的修改

---

## 类型选择指南

### 决策流程图

```
是否修改代码逻辑？
├─ 否 → docs（文档）或 style（格式）
└─ 是 → 是否修复 bug？
    ├─ 是 → fix
    └─ 否 → 是否添加新功能？
        ├─ 是 → feat
        └─ 否 → 是否改善性能？
            ├─ 是 → perf
            └─ 否 → 是否重构代码？
                ├─ 是 → refactor
                └─ 否 → 是否修改测试？
                    ├─ 是 → test
                    └─ 否 → chore / build / ci
```

### 常见组合

**实现 + 测试：**
```bash
# 分开提交
git commit user.py -m "feat(user): add profile update method"
git commit test_user.py -m "test(user): add profile update tests"
```

**重构 + 文档：**
```bash
git commit utils.py -m "refactor(utils): simplify validation logic"
git commit README.md -m "docs(readme): update validation examples"
```

**修复 + 测试：**
```bash
git commit parser.py -m "fix(parser): handle empty input"
git commit test_parser.py -m "test(parser): add test for empty input"
```

## 破坏性变更

当提交包含破坏性变更时，使用 `!` 或 `BREAKING CHANGE`：

```bash
# 方式 1: 在类型后添加 !
feat(api)!: remove deprecated user endpoint

# 方式 2: 在脚注中说明
feat(api): remove deprecated user endpoint

BREAKING CHANGE: The /api/v1/users endpoint is removed. Use /api/v2/users instead.
```

**破坏性变更包括：**
- 删除公共 API
- 修改函数签名
- 改变配置格式
- 更新依赖版本要求
- 修改数据结构

## 范围（Scope）的选择

范围是可选的，但提供额外的上下文信息：

### 常见的范围命名

**按模块划分：**
- `auth` - 认证授权
- `api` - API 接口
- `db` - 数据库
- `ui` - 用户界面
- `utils` - 工具函数

**按层次划分：**
- `controller` - 控制器层
- `service` - 服务层
- `model` - 模型层
- `view` - 视图层

**按功能划分：**
- `user` - 用户相关
- `payment` - 支付相关
- `notification` - 通知相关

### 范围命名建议

- 使用简短的名词或缩写
- 保持团队内部一致性
- 避免过于笼统（如 `code`）
- 避免过于具体（如 `line123`）

## 提交信息的最佳实践

### Subject（主题）的写作

**好的示例：**
```
feat(auth): add OAuth2 login support
fix(api): handle timeout errors
docs(readme): update installation guide
```

**不好的示例：**
```
feat: add stuff             # 太模糊
fix: fixed it              # 没说明什么问题
feat(auth): Added login    # 不应首字母大写
feat(auth): add login.     # 不应有句号
```

### Body（正文）的写作

当需要详细说明时，添加正文：

```
fix(database): resolve connection pool exhaustion

The connection pool was not releasing connections properly
when errors occurred during query execution.

Changes:
- Add try-finally blocks to ensure connection release
- Log connection pool metrics for monitoring
- Add timeout to prevent indefinite waiting

This issue was affecting production deployments under high load.

Refs: #123
```

### Footer（脚注）的使用

**常见的脚注类型：**

```
# 关联 Issue
Refs: #123
Closes: #456
Fixes: #789

# 审查者
Reviewed-by: @username
Acked-by: @username

# 破坏性变更
BREAKING CHANGE: API endpoint changed from /v1/users to /v2/users

# 性能影响
Performance: Query time reduced from 200ms to 50ms
```

## 常见错误

### 错误 1: 一个提交包含多个变更

**问题：**
```bash
git commit -m "feat: add authentication and update tests and fix typo"
```

**正确做法：**
```bash
git commit auth.py -m "feat(auth): add OAuth2 login"
git commit test_auth.py -m "test(auth): add login tests"
git commit README.md -m "docs(readme): fix typo"
```

### 错误 2: 类型选择不当

**问题：** 将 bug 修复标记为 feat
```bash
git commit -m "feat: fix login bug"
```

**正确做法：**
```bash
git commit -m "fix(auth): resolve token validation issue"
```

### 错误 3: 缺少上下文

**问题：**
```bash
git commit -m "fix: fix bug"
```

**正确做法：**
```bash
git commit -m "fix(auth): resolve token expiration issue"
```

### 错误 4: 过于笼统的范围

**问题：**
```bash
git commit -m "feat(code): add feature"
```

**正确做法：**
```bash
git commit -m "feat(auth): add OAuth2 support"
```

## 工具和自动化

### Commitlint

配置 commitlint 来验证提交信息：

```javascript
// commitlint.config.js
module.exports = {
  extends: ['@commitlint/config-conventional'],
  rules: {
    'type-enum': [
      2,
      'always',
      [
        'feat',
        'fix',
        'docs',
        'style',
        'refactor',
        'perf',
        'test',
        'chore',
        'build',
        'ci',
      ],
    ],
    'scope-enum': [2, 'always', ['auth', 'api', 'db', 'ui', 'utils']],
    'subject-max-length': [2, 'always', 50],
  },
};
```

### Git Hooks

使用 husky 添加 pre-commit hook：

```json
// package.json
{
  "husky": {
    "hooks": {
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  }
}
```

### 自动生成 Changelog

使用 conventional-changelog：

```bash
npm install -g conventional-changelog-cli
conventional-changelog -p angular -i CHANGELOG.md -s
```

## 总结

- **feat**: 新功能
- **fix**: Bug 修复
- **docs**: 文档变更
- **style**: 代码格式
- **refactor**: 重构
- **perf**: 性能优化
- **test**: 测试相关
- **chore**: 杂项
- **build**: 构建系统
- **ci**: CI 配置

记住：
1. 每个提交只做一件事
2. 使用清晰、描述性的信息
3. 遵循团队约定的格式
4. 提供足够的上下文信息
