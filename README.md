# 高考志愿通 - 智能大学推荐 Agent Web 应用

基于 CodeBuddy Agent SDK 构建的高考志愿填报推荐应用。输入**专业**和**分数**，AI 自动推荐全国公立大学可选方案（学校、地域、专业）。

## 功能特性

- **智能推荐**：根据专业方向和高考分数，自动推荐全国公立大学
- **三档分类**：按冲刺院校、稳妥院校、保底院校分类推荐
- **地域覆盖**：推荐结果覆盖全国不同省份和区域
- **专业匹配**：推荐与意向专业高度匹配的具体专业及交叉学科
- **多 Agent 模式**：内置高考志愿推荐专家、专业解读助手、院校对比分析三种模式
- **实时流式响应**：AI 回答实时流式显示
- **会话管理**：支持多会话，历史记录持久化（SQLite）
- **双模式运行**：支持 Web 浏览器开发和 Electron 桌面应用

## 技术栈

- **前端**：React 18 + TypeScript + Vite 5 + TDesign React + Tailwind CSS
- **后端**：Express 4 + CodeBuddy Agent SDK + SSE 流式通信
- **数据库**：SQLite（会话和消息持久化）
- **桌面**：Electron（可选桌面封装）

## 快速开始

### 1. 安装依赖

```bash
npm install --legacy-peer-deps
```

### 2. 配置环境变量

```bash
cp .env.example .env
```

编辑 `.env` 文件，填入你的 CodeBuddy API Key：

```
CODEBUDDY_API_KEY=your_api_key_here
```

> API Key 从 https://www.codebuddy.cn 获取

### 3. Web 浏览器开发模式

```bash
npm run dev
```

- 前端：http://localhost:5173
- 后端 API：http://localhost:3000

### 4. Electron 桌面开发模式

先单独安装 Electron 依赖（避免安装冲突）：

```bash
npm install electron electron-builder wait-on --legacy-peer-deps
```

然后启动：

```bash
npm run electron:dev
```

## 使用说明

1. 打开应用后，在首页选择**专业**（支持搜索，涵盖工科、理科、文史、经管、法学、医学、教育、农学、艺术 9 大类）
2. 输入**高考分数**
3. 可选：选择**所在省份**和**考试科类**（提高推荐精度）
4. 选择助手模式（默认为"高考志愿推荐专家"）
5. 点击**「生成大学推荐方案」**，AI 将自动生成推荐

## 项目结构

```
college-admission-agent/
├── electron/               # Electron 桌面应用
│   ├── main.cjs           # 主进程
│   └── preload.cjs        # 预加载脚本
├── server/                 # 后端
│   ├── index.ts           # Express + SSE 服务器
│   └── db.ts              # SQLite 数据库操作
├── src/                    # 前端
│   ├── components/        # UI 组件
│   │   ├── NewChatView.tsx    # 首页表单（专业+分数输入）
│   │   ├── ChatMessages.tsx   # 消息展示
│   │   ├── ChatInput.tsx      # 输入框
│   │   ├── Header.tsx         # 顶部栏
│   │   ├── Sidebar.tsx        # 侧边栏
│   │   └── ...
│   ├── hooks/             # React Hooks
│   ├── pages/             # 页面
│   ├── config.ts          # 应用配置
│   ├── types.ts           # 类型定义
│   └── main.tsx           # 入口
├── data/                   # SQLite 数据存储
├── package.json
├── vite.config.ts
└── .env.example
```

## 内置 Agent

| Agent | 描述 | 图标 |
|-------|------|------|
| 高考志愿推荐专家 | 根据专业和分数推荐全国公立大学 | GraduationCap |
| 专业解读助手 | 详细解读各专业培养方向、就业前景 | BookOpen |
| 院校对比分析 | 对比多所高校的优劣势 | Scale |

## NPM 脚本

| 命令 | 说明 |
|------|------|
| `npm run dev` | Web 浏览器开发（前后端同时启动） |
| `npm run dev:server` | 仅启动后端服务器 |
| `npm run dev:client` | 仅启动前端开发服务器 |
| `npm run build` | 构建前端生产版本 |
| `npm run electron:dev` | Electron 桌面开发模式 |
| `npm run electron:build` | 构建 Electron 桌面安装包 |
| `npm run electron:preview` | 预览 Electron 生产构建 |

## 环境变量

| 变量名 | 说明 | 必填 |
|--------|------|------|
| `CODEBUDDY_API_KEY` | CodeBuddy API Key | 是 |
| `CODEBUDDY_AUTH_TOKEN` | CodeBuddy Auth Token（与 API Key 二选一） | 否 |
| `CODEBUDDY_BASE_URL` | 自定义 Base URL | 否 |
| `PORT` | 后端服务器端口（默认 3000） | 否 |

## 注意事项

- 推荐结果仅供参考，实际录取情况请以各高校官方招生信息为准
- 需要有效的 CodeBuddy API Key 才能使用 AI 推荐功能
- Electron 打包需要先安装 `electron` 和 `electron-builder`
