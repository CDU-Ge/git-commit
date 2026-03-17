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

---

# 自动化提交流程

## 执行步骤

当用户要求提交变更时，按以下流程自动执行，无需询问。

### 1. 分析变更

```bash
git status
git diff --stat
```

### 2. 读取变更内容

对每个已修改的文件，执行 `git diff <file>` 分析变更内容。

### 3. 自动分组文件

按以下规则分组：

- **测试文件**：`tests/**/*.py`, `test_*.py`, `*.test.ts`, `*.spec.js` → 独立分组
- **文档文件**：`*.md`, `README`, `CHANGELOG`, `*.txt` → 独立分组
- **配置文件**：`*.json`, `*.yaml`, `*.yml`, `*.toml`, `.*rc` → 独立分组
- **锁文件**：`*-lock.json`, `Cargo.lock`, `Gemfile.lock`, `poetry.lock` → 独立分组
- **代码文件**：按目录或模块分组

### 4. 确定提交类型和范围

根据文件路径和 diff 内容自动判断：

| 文件路径 | 类型 | 范围 |
|---------|------|------|
| `tests/` | test | 从路径提取模块名 |
| `*.md`, `docs/` | docs | 文件名或目录名 |
| `*.json`, `*.yaml` | chore | config |
| `*-lock.json` | chore | deps |
| `.github/`, `.gitlab-ci.yml` | ci | ci |
| `src/`, `lib/` | 分析代码变更 | 从路径提取模块名 |

### 5. 生成提交信息

格式：`<type>(<scope>): <subject>`

- type：从上表确定
- scope：从文件路径提取（如 auth, api, user）
- subject：根据 diff 内容生成，使用动词开头

### 6. 执行提交

按分组依次提交：

```bash
git add <files>
git commit <files> -m "<type>(<scope>): <subject>"
```

## 分组示例

假设变更文件：
- `src/auth/login.py`
- `src/auth/oauth.py`
- `tests/auth_test.py`
- `README.md`
- `package-lock.json`

分组结果：
```bash
git commit src/auth/login.py src/auth/oauth.py -m "feat(auth): add OAuth2 login"
git commit tests/auth_test.py -m "test(auth): add OAuth2 tests"
git commit README.md -m "docs(readme): update installation"
git commit package-lock.json -m "chore(deps): update dependencies"
```

## 快速决策流程

```
是否修改代码逻辑？
├─ 否 → docs 或 chore
│   ├─ 文档文件 → docs
│   └─ 配置/锁文件 → chore
└─ 是 → 代码文件
    ├─ 添加新功能/新增代码 → feat
    ├─ 修复错误/边界情况 → fix
    ├─ 重命名/提取/重组代码 → refactor
    └─ 优化性能/缓存 → perf
```
