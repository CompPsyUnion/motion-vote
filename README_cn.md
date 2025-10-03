# Motion Vote - 辩论活动实时投票互动系统

<div align="center">

![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)
![Version](https://img.shields.io/badge/version-1.0.0-green.svg)
![Build](https://img.shields.io/badge/build-passing-brightgreen.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

## **为辩论赛事打造的完整实时投票互动解决方案**

[功能特性](#-功能特性) • [快速开始](#-快速开始) • [技术架构](#️-技术架构) • [文档](#-文档) • [贡献指南](#-贡献指南)

</div>

---

## 📖 项目简介

辩论活动实时投票互动系统是一套专为辩论赛事设计的完整解决方案，旨在为活动组织者提供高效的活动管理工具，为现场观众提供便捷的投票互动体验，并通过大屏实时展示投票数据，全面提升辩论活动的互动性和观赏性。

### 核心价值

- **🎯 高效管理** - 为主办方提供完善的活动管理和协同工具，降低组织成本
- **👥 便捷参与** - 观众无需注册，扫码即可参与投票，随时表达观点
- **📊 实时展示** - 大屏实时可视化呈现投票数据，增强现场氛围
- **🔒 安全可靠** - 多重防刷票机制，数据加密传输，确保投票公平性
- **📈 数据分析** - 完整的投票数据追溯和分析报告，支持数据导出

---

## ✨ 功能特性

### 🎪 活动管理

- **活动创建与配置** - 支持创建辩论活动，配置活动信息、时间、地点等
- **协作管理** - 邀请多人协同管理活动，支持细粒度权限控制
- **参与者管理** - 批量导入参与者，生成个性化门票二维码
- **活动设置** - 灵活配置改票规则、数据展示方式、大屏主题等

### 🎭 辩题管理

- **辩题创建** - 为活动添加多个辩题，支持正反方观点描述
- **状态控制** - 实时控制辩题状态（待开始/辩论中/最终投票/已结束）
- **一键切换** - 后台快速切换当前展示辩题，大屏同步更新
- **灵活排序** - 支持拖拽调整辩题顺序

### 🗳️ 投票系统

- **快速入场** - 扫描门票二维码或输入编号即可进入活动
- **初始投票** - 辩论开始前进行立场投票（正方/反方/弃权）
- **实时改票** - 辩论过程中可随时改变立场，记录完整改票历史
- **投票锁定** - 辩题结束后自动锁定结果，防止篡改
- **防刷票机制** - IP 限流、设备指纹、异常行为监控多重防护

### 📺 大屏展示

- **实时数据更新** - WebSocket 推送，延迟小于 1 秒
- **多种展示模式** - 支持显示当前辩题、正方情况、反方情况、双方对比
- **丰富的可视化** - 票数统计、百分比、改票流向、趋势图表
- **主题定制** - 提供经典版、科技版、简约版等多种主题
- **远程控制** - 后台可远程控制大屏显示内容

### 📊 数据统计

- **实时看板** - 查看实时在线人数、投票统计、参与者活跃度
- **活动报告** - 自动生成包含完整数据分析的活动报告
- **数据导出** - 支持导出 PDF 报告、Excel 数据明细

---

## 🏗️ 技术架构

### 技术栈

#### **前端技术**

- Vue 3 + TypeScript - 现代化前端框架
- ECharts - 数据可视化图表
- Pinia - 状态管理
- Socket.io-client - WebSocket 实时通信

#### **后端技术**

- Python + FastAPI - Web 框架
- MySQL 8.0 - 关系型数据库
- Redis - 缓存与会话管理
- Socket.io / WebSocket - 实时数据推送
- JWT - 身份认证与授权

#### **部署运维**

- Docker - 容器化部署
- Nginx - 反向代理与负载均衡

---

## 🚀 快速开始

### 环境要求

- Node.js >= 20.x
- MySQL >= 8.0
- Redis >= 6.0

### 安装步骤

#### 1. 克隆项目

```bash
git clone https://github.com/comppsyunion/motion-vote.git
cd motion-vote
```

#### 2. 安装依赖

```bash
# 安装前端依赖
cd frontend
npm install

# 安装后端依赖
cd ../backend
npm install
```

#### 3. 初始化数据库

待完善(WIP)

#### 4. 启动服务

```bash
# 启动后端服务
cd backend
python main.py

# 启动前端服务
cd frontend
pnpm dev
```

### Docker 快速部署

#### 配置环境变量和 SMToGo 相关

在与 `docker-compose.yml` 文件同级目录下创建一个 `config` 目录，并添加一个 `smtp_config.jsonc` 文件，内容如下：

```jsonc
// 根据需要修改以下配置
{
    // API Configuration
    "api_key": "", // API key for authentication (leave empty to disable)
    "api_name": "High-Performance SMTP API", // API name
    "api_description": "SMTP API mail dispatch with support for attachments.", // API description
    // SMTP Server Settings
    "smtp_server": "maildev.com", // SMTP server hostname (for docker: service name)
    "smtp_port": 1025, // SMTP port
    "use_ssl": false, // Use SSL/TLS encryption
    "use_password": false, // Whether to authenticate with username/password
    "use_tls": false, // Use STARTTLS
    // Email Limits
    "max_len_recipient_email": 64, // Maximum length for recipient email
    "max_len_subject": 255, // Maximum subject length
    "max_len_body": 50000, // Maximum email body length
    // Sender Configuration
    "sender_email": "your_email@example.com", // SMTP authentication email (actual account)
    "sender_email_display": "", // From header display email (leave empty to use sender_email)
    "sender_domain": "devel.local.email",
    "sender_password": "your_password"
}
```

以及一个 `data` 目录用于存放 smtogo 日志文件。

在 `docker-compose.yml` 中配置数据库和 Redis 连接信息（如果需要）。

```yaml
    environment:
      - DATABASE_URL=postgresql://postgres-url:your-password@motion-vote-db:5432/motionvote
      - REDIS_URL=redis://motion-vote-redis:6379/0
```

```bash
# 构建并启动所有服务
docker-compose up -d

# 查看服务状态
docker-compose ps

# 查看日志
docker-compose logs -f
```

---

## 📚 文档

### 核心概念

#### **系统角色**

- **系统管理员** - 管理所有用户和系统配置
- **活动主办方** - 创建和管理辩论活动
- **协作管理员** - 协助主办方管理活动
- **现场观众** - 无需注册，扫码参与投票
- **大屏展示** - 实时展示投票数据

#### **辩题状态流转**

```mermaid
graph LR
    A[待开始] --> B[辩论中]
    B --> C[最终投票]
    C --> D[已结束]
```

### API 文档

API 文档正在梳理中

### 配置说明

#### **活动配置项**

| 配置项                | 说明               | 默认值  |
| --------------------- | ------------------ | ------- |
| `allowChangeVote`     | 是否允许改票       | true    |
| `maxChangeCount`      | 最大改票次数       | 3       |
| `showRealTimePercent` | 是否显示实时百分比 | true    |
| `screenTheme`         | 大屏主题           | classic |

#### 关于管理员

首次注册用户即为管理员，拥有所有权限。管理员可为其他用户分配管理员角色。

---

## 🔐 安全性

### 防刷票机制

- **IP 限流** - 单个 IP 每分钟最多投票 10 次
- **设备指纹识别** - 防止同一设备多次投票
- **异常行为监控** - 自动识别异常投票模式
- **参与者验证** - 唯一的活动 ID 和参与者编号组合

---

## 📦 部署

### 生产环境部署

#### 1. 构建项目

```bash
# 构建前端
cd frontend
npm run build

# 构建后端
cd ../backend
npm run build
```

#### 2. 使用 Docker 部署

待完善(WIP)

#### 3. Nginx 配置示例

```nginx
server {
    listen 80;
    server_name yourdomain.com;

    # 前端静态文件
    location / {
        root /var/www/debate-voting/dist;
        try_files $uri $uri/ /index.html;
    }

    # API代理
    location /api {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    # WebSocket代理
    location /socket.io {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

### 性能优化建议

- 启用 Redis 缓存热点数据
- 配置 MySQL 读写分离
- 使用 CDN 加速静态资源
- 开启 Gzip 压缩
- 配置负载均衡（多实例部署）

---

## 🤝 贡献指南

我们欢迎任何形式的贡献！在提交 PR 之前，请阅读以下指南：

### 开发流程

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 提交 Pull Request

### 代码规范

- 使用 ESLint 和 Prettier 格式化代码
- 遵循 Vue 3 官方风格指南
- 编写清晰的提交信息
- 为新功能添加单元测试
- 更新相关文档

### 提交信息规范

```text
<type>(<scope>): <subject>

<body>

<footer>
```

#### **Type 类型**

- `feat`: 新功能
- `fix`: 修复 bug
- `docs`: 文档更新
- `style`: 代码格式调整
- `refactor`: 重构
- `test`: 测试相关
- `chore`: 构建工具或辅助工具的变动

### 报告问题

如果您发现 bug 或有功能建议，请[提交 Issue](https://github.com/comppsyunion/motion-vote/issues)。

提交 Issue 时请包含：

- 问题的详细描述
- 复现步骤
- 期望行为
- 实际行为
- 系统环境信息

---

## 📄 开源协议

本项目采用 [Apache License 2.0](LICENSE) 开源协议。

---

## 👥 团队

- **项目负责人**: [@buduan](https://github.com/buduan), [@hnrobert](https://github.com/hnrobert)
- **核心开发者**: 查看 [贡献者列表](https://github.com/comppsyunion/motion-vote/graphs/contributors)

---

## 🙏 致谢

感谢所有为本项目做出贡献的开发者！

特别感谢以下开源项目：

- [Vue.js](https://vuejs.org/)
- [ECharts](https://echarts.apache.org/)
- [Socket.io](https://socket.io/)

---

## 📧 联系我们

- **团队邮箱**: <computerpsychounion@nottingham.edu.cn>
- **开发者邮箱**: 不断同学 <buduan461@gmail.com>; Robert He <hnrobert@qq.com>

---

## 🌟 Star History

如果这个项目对您有帮助，请给我们一个 ⭐️ Star！

[![Star History Chart](https://api.star-history.com/svg?repos=comppsyunion/motion-vote&type=Date)](https://star-history.com/#CompPsyUnion/Motion-Vote&Date)

---

<div align="center">

Made with ❤️ by Computer Psycho Union

</div>
