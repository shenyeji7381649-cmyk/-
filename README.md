# 项目入门（React + Node.js + PostgreSQL）

> 本仓库目前仍在初始化阶段：文档已就绪，业务代码待落地。本文目标是让新人 **7 天内完成首个可合并 PR**。

---

## 0. 你要先知道的事实

- 当前仓库已有 onboarding 文档，但尚未建立 `frontend/`、`backend/`、`db/` 的实际工程目录。
- 因此“下一步”不是继续写抽象文档，而是把文档中的结构与流程转成可运行项目。

---

## 1. 推荐目录结构（待落地）

```text
.
├── frontend/                 # React 应用（建议 Vite）
│   ├── src/
│   ├── public/
│   └── package.json
├── backend/                  # Node.js API（Express/Fastify）
│   ├── src/
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── services/
│   │   ├── repositories/
│   │   └── middlewares/
│   ├── tests/
│   └── package.json
├── db/
│   ├── migrations/           # schema 变更
│   └── seeds/                # 初始化数据
├── docs/
│   └── architecture.md
├── CONTRIBUTING.md
└── README.md
```

---

## 2. 技术栈职责边界

- **React（frontend）**：页面渲染、交互、状态与 API 调用。
- **Node.js（backend）**：接口协议、鉴权、业务规则、错误处理。
- **PostgreSQL（db）**：数据持久化、索引、事务、约束。

**边界原则**：
- 前端不写业务真规则（只做展示与编排）
- Controller 不直写 SQL
- Service 不关心 HTTP 细节

---

## 3. 新人 7 天可执行计划（建议）

### Day 1：环境准备
- 安装 Node.js LTS、PostgreSQL、包管理器（npm/pnpm）
- 复制 `.env.example`（后续补齐）并启动本地数据库

### Day 2：工程骨架初始化
- 创建 `frontend`（React）和 `backend`（Node.js）
- 后端提供 `/health` 路由，前端可访问到该路由

### Day 3：数据库接入
- 新建首条 migration（例如 `todos` 表）
- 加入 seed 数据，完成本地初始化

### Day 4：首条业务链路
- 完成 `GET /api/todos`
- 前端列表页展示返回数据

### Day 5：质量补齐
- 后端至少 1 条单元测试 + 1 条集成测试
- 前端至少 1 条组件测试（可选）

### Day 6：工程化
- 加 lint/test/build 脚本
- 接入 CI（PR 触发）

### Day 7：首个 PR
- 提交“端到端最小链路”PR
- 按 `CONTRIBUTING.md` 模板补齐背景、风险与验证

---

## 4. 首个端到端任务（建议就做这个）

**目标**：完成 Todo 列表最小链路。

- 数据库：`todos(id, title, completed, created_at)`
- 后端：`GET /api/todos` 返回 `[{ id, title, completed }]`
- 前端：`/todos` 页面展示列表 + 空态
- 验收：页面可见 seed 数据；接口异常有统一错误响应

### Definition of Done（DoD）
- [ ] 本地可一键启动（至少两条命令：前端 / 后端）
- [ ] migration 可执行，seed 可重跑
- [ ] PR 中附验证命令与结果
- [ ] lint/test/build 全通过

---

## 5. 本地配置参考

### backend/.env（示例）

```bash
NODE_ENV=development
PORT=3001
DATABASE_URL=postgres://postgres:postgres@localhost:5432/app_dev
JWT_SECRET=replace_me
LOG_LEVEL=info
```

### frontend/.env（示例）

```bash
VITE_API_BASE_URL=http://localhost:3001
```

---

## 6. 常用命令（示例）

```bash
# frontend
cd frontend
npm install
npm run dev

# backend
cd backend
npm install
npm run dev

# test / lint / build（后续需在 package.json 中落地）
npm test
npm run lint
npm run build
```

---

## 7. 常见风险与规避

- **风险：文档先行但代码未落地**
  - 规避：优先做最小端到端链路，不继续扩写抽象文档。
- **风险：接口返回不统一**
  - 规避：统一错误码与错误响应结构。
- **风险：数据库变更不可追踪**
  - 规避：所有 schema 变更必须走 migration。

---

## 8. 下一步优先级（只做 3 件）

1. 建立真实 `frontend/` + `backend/` + `db/` 目录骨架。
2. 完成 Todo 端到端链路（页面 -> API -> DB）。
3. 接入 CI 门禁（lint/test/build）。
