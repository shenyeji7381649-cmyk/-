# 架构说明（React + Node.js + PostgreSQL）

## 1. 高层架构

```text
[ Browser / React ]
        |
        | HTTP(JSON)
        v
[ Node.js API ]
        |
        | SQL / ORM
        v
[ PostgreSQL ]
```

职责：
- React：交互与视图
- Node.js：业务逻辑与接口编排
- PostgreSQL：事务与持久化

## 2. 推荐后端分层

- `routes/`：路由注册、参数入口
- `controllers/`：请求编排、响应组装
- `services/`：核心业务规则
- `repositories/`：数据读写
- `middlewares/`：鉴权、日志、统一错误处理

**约束建议：**
- Controller 不直连数据库
- Service 不依赖 HTTP 对象
- Repository 只负责数据访问，不混入业务规则

## 3. 前端模块建议

- `pages/`：页面容器
- `components/`：复用 UI 组件
- `api/`：请求封装
- `hooks/`：状态与副作用复用
- `store/`：全局状态（如有）

## 4. 接口与错误处理建议

### 响应结构（示例）

```json
{
  "success": true,
  "data": {},
  "requestId": "xxx"
}
```

```json
{
  "success": false,
  "error": {
    "code": "INVALID_PARAM",
    "message": "title is required"
  },
  "requestId": "xxx"
}
```

## 5. 非功能性要求（首期）

- **可观测性**：请求日志、错误日志、requestId 贯通
- **安全性**：输入校验、鉴权、最小权限
- **性能**：分页、索引、慢查询排查
- **可维护性**：统一风格、分层清晰、可测试

## 6. 30/60/90 天演进建议

### 0~30 天
- 打通 1 条主链路并建立 CI
- 规范日志与错误处理

### 31~60 天
- 增加鉴权体系与权限模型
- 完善测试金字塔（单元/集成/e2e）

### 61~90 天
- 缓存与异步任务（队列）
- 数据库读写优化与容量评估
