# 约定式提交 1.0.0

## 概述

约定式提交规范是一种轻量级约定，提供简单规则创建清晰的提交历史。

## 结构

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## 类型

- feat: 新功能（对应 SemVer MINOR）
- fix: 修复 bug（对应 SemVer PATCH）
- BREAKING CHANGE: 破坏性变更（对应 SemVer MAJOR）

其他类型：build、chore、ci、docs、style、refactor、perf、test

## 示例

### 破坏性变更

```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

### 使用 !

```
feat!: send an email to the customer when a product is shipped
```

### 包含范围

```
feat(lang): add polish language
```

### 包含正文和脚注

```
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Reviewed-by: Z
Refs: #123
```

## 规范

1. 必须使用类型字段前缀，后接可选范围、可选 !、冒号和空格
2. 新功能必须使用 feat
3. 修复 bug 必须使用 fix
4. 范围必须是用圆括号包围的名词
5. 描述必须直接跟在前缀冒号空格后
6. 正文必须起始于描述结束的空行后
7. 脚注每行必须包含令牌、`:<space>` 或 `<space>#` 分隔符、值
8. 破坏性变更必须用 BREAKING CHANGE: 或 ! 标记
9. 工具实现必须不区分大小写（BREAKING CHANGE 除外）

## 为什么使用

- 自动化生成 CHANGELOG
- 自动决定语义化版本
- 传达变更性质
- 触发构建和部署
- 结构化的提交历史
