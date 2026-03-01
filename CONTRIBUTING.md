# 贡献指南（Contributing）

用于统一 React + Node.js + PostgreSQL 项目协作方式。

## 1. 分支与提交规范

- 分支命名：
  - `feat/<short-name>`：新功能
  - `fix/<short-name>`：缺陷修复
  - `chore/<short-name>`：工程维护
  - `docs/<short-name>`：文档改进

- 提交信息建议使用 Conventional Commits：
  - `feat: ...`
  - `fix: ...`
  - `docs: ...`
  - `refactor: ...`
  - `test: ...`

## 2. PR 最低质量要求

提交 PR 前至少满足：

1. 本地可运行（前后端）
2. lint / test / build 通过
3. 改动有对应测试（文档改动可除外）
4. 涉及 schema 变更必须附 migration

## 3. PR 描述模板（建议）

### 背景
- 为什么要做这次改动？

### 变更内容
- 具体新增/修改了哪些点？

### 风险评估
- 是否影响接口兼容性？
- 是否涉及数据库变更？
- 回滚方案是什么？

### 验证记录
- 执行命令：
  - `npm run lint`
  - `npm test`
  - `npm run build`
- 核心场景验证结果：

## 4. 代码评审关注点

- 模块边界是否清晰（UI/API/Service/DB）
- 是否有可抽象的重复逻辑
- 异常分支与空数据是否处理完整
- SQL 是否考虑索引、分页与 N+1 风险
- 是否有敏感信息泄露风险（日志、响应）

## 5. 数据库变更约定

- 禁止手工改线上 schema
- schema 变更必须通过 migration
- 迁移脚本应可重复执行（或有明确回滚）
- 大表变更需评估锁表时间与执行窗口

## 6. 紧急修复（hotfix）建议流程

1. 从稳定分支切 `fix/hotfix-xxx`
2. 最小化改动并补关键测试
3. 合并后立刻回合并到开发分支，避免分叉
