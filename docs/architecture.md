# 架构说明（React + Node.js + PostgreSQL）

## 1. 总体架构

```text
[ Browser / React ]
        |
        | HTTP (JSON)
        v
[ Node.js API Layer ]
        |
        | SQL / ORM
        v
[ PostgreSQL ]
```

- React 负责交互与展示
- Node.js 负责业务逻辑与接口编排
- PostgreSQL 负责持久化与事务一致性

## 2. 推荐分层（后端）

- `routes/`：路由与基础参数解析
- `controllers/`：请求编排与响应组装
- `services/`：核心业务逻辑
- `repositories/` 或 `db/`：数据访问
- `middlewares/`：鉴权、日志、错误处理

> 原则：控制器薄、服务层稳、数据访问可替换。

## 3. 前端模块建议

- `pages/`：页面级组件
- `components/`：可复用组件
- `api/`：接口封装
- `hooks/`：复用逻辑
- `store/`：全局状态（如有）

> 原则：页面只做编排，副作用尽量收敛到 hooks 或 api 层。

## 4. 关键非功能性要求

- **可观测性**：请求日志、错误日志、关键指标
- **安全性**：鉴权、输入校验、最小权限
- **可维护性**：统一代码风格、清晰分层
- **性能**：接口分页、缓存策略、SQL 索引

## 5. 演进建议

1. 先保证一条主业务链路稳定可回归
2. 再抽象通用能力（鉴权、错误处理、日志）
3. 最后再做高级优化（缓存、异步任务、读写分离）
