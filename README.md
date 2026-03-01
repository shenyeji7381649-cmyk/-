# 项目入门（React + Node.js + PostgreSQL）

这是一个基于 **React（前端）+ Node.js（后端）+ PostgreSQL（数据库）** 的全栈项目模板型说明文档，目标是帮助新人在最短时间内完成：

1. 理解仓库结构
2. 本地启动开发环境
3. 跑通测试与基本开发流程

---

## 1. 建议的仓库结构

> 当前仓库处于初始化阶段，下面是推荐结构（可按实际项目逐步对齐）。

```text
.
├── frontend/                 # React 应用
│   ├── src/
│   ├── public/
│   └── package.json
├── backend/                  # Node.js 服务
│   ├── src/
│   │   ├── routes/
│   │   ├── services/
│   │   ├── db/
│   │   └── app.ts|js
│   ├── tests/
│   └── package.json
├── db/
│   ├── migrations/           # SQL 迁移
│   └── seeds/                # 初始化数据
├── docs/
│   └── architecture.md       # 架构说明
├── CONTRIBUTING.md           # 协作规范
└── README.md
```

---

## 2. 技术栈职责划分

- **React（frontend）**
  - 页面、组件、路由、状态管理
  - 调用后端 API，渲染业务数据
- **Node.js（backend）**
  - 提供 REST API / GraphQL API
  - 业务逻辑、权限控制、参数校验
  - 与 PostgreSQL 交互
- **PostgreSQL（db）**
  - 存储核心业务数据
  - 管理 schema、索引、事务一致性

---

## 3. 新人第一周建议学习路径

### Day 1：跑起来
- 安装 Node.js（建议 LTS）与 PostgreSQL
- 分别启动 frontend / backend
- 确认前端能访问后端健康检查接口（例如 `/health`）

### Day 2~3：看主链路
- 找到一个核心页面（例如列表页）
- 追踪一次完整请求：
  - React 页面触发请求
  - Node.js 路由接收并处理
  - PostgreSQL 查询返回
  - 前端渲染结果

### Day 4~5：做一个小改动并提 PR
- 改一个低风险需求（例如增加字段展示、优化校验）
- 补充对应测试
- 按 `CONTRIBUTING.md` 提交 PR

---

## 4. 本地开发建议

### 环境变量（示例）

后端常见环境变量（放在 `backend/.env`）：

```bash
NODE_ENV=development
PORT=3001
DATABASE_URL=postgres://postgres:postgres@localhost:5432/app_dev
JWT_SECRET=replace_me
```

前端常见环境变量（放在 `frontend/.env`）：

```bash
VITE_API_BASE_URL=http://localhost:3001
# 或 CRA 风格: REACT_APP_API_BASE_URL=http://localhost:3001
```

### 常用命令（示例）

```bash
# frontend
cd frontend
npm install
npm run dev

# backend
cd backend
npm install
npm run dev

# backend test
npm test
```

---

## 5. 关键工程实践（建议尽快落地）

- 接口参数校验（如 zod/joi）
- 错误处理统一化（统一 error response）
- 数据库迁移规范化（每个 schema 变更有 migration）
- PR 必跑检查：lint + test + build
- 重要模块补充 README（例如 `backend/src/services/README.md`）

---

## 6. 新人高频问题

1. **问题：从哪里开始看代码？**
   - 从一个业务页面出发，沿着 API 请求路径读到数据库层。
2. **问题：哪些模块最关键？**
   - 鉴权、订单/核心业务服务、数据库迁移、全局错误处理。
3. **问题：如何判断改动是否安全？**
   - 是否有测试覆盖；是否影响接口兼容性；是否需要数据迁移。

---

## 7. 下一步可执行项

- 建立实际 `frontend/` 与 `backend/` 目录骨架
- 补充一条完整样例链路（页面 -> API -> DB）
- 增加 CI（至少包含 `npm run lint`、`npm test`、`npm run build`）
