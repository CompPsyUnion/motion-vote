# Motion Vote - Real-time Voting Interaction System for Debate Events

<div align="center">

![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)
![Version](https://img.shields.io/badge/version-1.0.0-green.svg)
![Build](https://img.shields.io/badge/build-passing-brightgreen.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

## **A complete real-time voting solution designed for debate competitions**

[Features](#-features) • [Quick Start](#-quick-start) • [Architecture](#️-architecture) • [Docs](#api-docs) • [Contributing](#-contributing)

</div>

---

## 📖 Project Overview

Motion Vote is a comprehensive solution tailored for debate events, aiming to provide organizers with efficient management tools, offer audiences a convenient voting experience, and display real-time voting data on big screens to enhance interactivity and engagement throughout the event.

### Core Values

- **🎯 Efficient Management** - Complete event management and collaboration tools for organizers, reducing operational costs
- **👥 Easy Participation** - Audiences can vote instantly by scanning a QR code, no registration required
- **📊 Real-time Display** - Big screen visualizes voting data in real time, boosting event atmosphere
- **🔒 Secure & Reliable** - Multiple anti-cheating mechanisms and encrypted data transmission ensure fairness
- **📈 Data Analytics** - Full voting data traceability and analysis reports, with export support

---

## ✨ Features

### 🎪 Event Management

- **Event Creation & Configuration** - Create debate events, configure info, time, location, etc.
- **Collaboration Management** - Invite multiple users to co-manage events, with fine-grained permissions
- **Participant Management** - Bulk import participants, generate personalized ticket QR codes
- **Event Settings** - Flexible rules for vote changing, data display, big screen themes, etc.

### 🎭 Motion Management

- **Motion Creation** - Add multiple motions to events, support for pro/con descriptions
- **Status Control** - Real-time control of motion status (Not Started/In Progress/Final Vote/Ended)
- **One-click Switch** - Quickly switch current motion in admin, big screen syncs instantly
- **Flexible Sorting** - Drag-and-drop to reorder motions

### 🗳️ Voting System

- **Quick Entry** - Enter event by scanning ticket QR or entering code
- **Initial Voting** - Vote for side (Pro/Con/Abstain) before debate starts
- **Real-time Vote Change** - Change side anytime during debate, with full change history
- **Vote Locking** - Results auto-locked after motion ends, preventing tampering
- **Anti-cheating** - IP rate limiting, device fingerprinting, abnormal behavior monitoring

### 📺 Big Screen Display

- **Real-time Data Update** - WebSocket push, latency <1s
- **Multiple Display Modes** - Show current motion, pro/con status, comparison, etc.
- **Rich Visualization** - Vote counts, percentages, change flows, trend charts
- **Theme Customization** - Classic, Tech, Minimalist and more themes
- **Remote Control** - Admin can remotely control big screen content

### 📊 Data Analytics

- **Real-time Dashboard** - View online users, vote stats, participant activity
- **Event Reports** - Auto-generate full data analysis reports
- **Data Export** - Export PDF reports, Excel details

---

## 🏗️ Architecture

### Tech Stack

#### **Frontend**

- Vue 3 + TypeScript - Modern frontend framework
- ECharts - Data visualization
- Pinia - State management
- Socket.io-client - Real-time WebSocket communication

#### **Backend**

- Python + FastAPI - Web framework
- MySQL 8.0 - Relational database
- Redis - Cache & session management
- Socket.io / WebSocket - Real-time data push
- JWT - Authentication & authorization

#### **Deployment & Ops**

- Docker - Containerized deployment
- Nginx - Reverse proxy & load balancing

---

## 🚀 Quick Start

### Requirements

- Node.js >= 20.x
- MySQL >= 8.0
- Redis >= 6.0

### Installation Steps

#### 1. Clone the Project

```bash
git clone https://github.com/comppsyunion/motion-vote.git
cd motion-vote
```

#### 2. Install Dependencies

```bash
# Frontend dependencies
cd frontend
npm install

# Backend dependencies
cd ../backend
npm install
```

#### 3. Initialize Database

To be completed (WIP)

#### 4. Start Services

```bash
# Start backend service
cd backend
python main.py

# Start frontend service
cd frontend
pnpm dev
```

### Docker Quick Deploy

```bash
# Build and start all services
docker-compose up -d

# Check service status
docker-compose ps

# View logs
docker-compose logs -f
```

---

## 📚 Documentation

### Core Concepts

#### **System Roles**

- **System Admin** - Manages all users and system settings
- **Event Organizer** - Creates and manages debate events
- **Co-admin** - Assists organizer in event management
- **Audience** - No registration, join and vote via QR code
- **Big Screen** - Real-time vote data display

#### **Motion Status Flow**

```mermaid
flowchart LR
    A[Not Started] --> B[In Progress]
    B --> C[Final Vote]
    C --> D[Ended]

### API Docs

API documentation is in progress.

### Configuration

**Event Config Options**

| Option                | Description               | Default |
| --------------------- | ------------------------- | ------- |
| `allowChangeVote`     | Allow vote changing       | true    |
| `maxChangeCount`      | Max vote changes          | 3       |
| `showRealTimePercent` | Show real-time percentage | true    |
| `screenTheme`         | Big screen theme          | classic |

---

## 🔐 Security

### Anti-cheating Mechanisms

- **IP Rate Limiting** - Max 10 votes per IP per minute
- **Device Fingerprinting** - Prevent multiple votes from same device
- **Abnormal Behavior Monitoring** - Auto-detect suspicious voting patterns
- **Participant Verification** - Unique event ID and participant code combo

---

## 📦 Deployment

### Production Deployment

#### 1. Build Project

```bash
# Build frontend
cd frontend
npm run build

# Build backend
cd ../backend
npm run build
```

#### 2. Deploy with Docker

To be completed (WIP)

#### 3. Nginx Config Example

```nginx
server {
    listen 80;
    server_name yourdomain.com;

    # Frontend static files
    location / {
        root /var/www/debate-voting/dist;
        try_files $uri $uri/ /index.html;
    }

    # API proxy
    location /api {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    # WebSocket proxy
    location /socket.io {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

### Performance Optimization

- Enable Redis cache for hot data
- Configure MySQL read/write splitting
- Use CDN for static assets
- Enable Gzip compression
- Set up load balancing (multi-instance deployment)

---

## 🤝 Contributing

We welcome all forms of contribution! Please read the following guidelines before submitting a PR:

### Development Workflow

1. Fork this repo
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Submit a Pull Request

### Code Style

- Use ESLint and Prettier for code formatting
- Follow Vue 3 official style guide
- Write clear commit messages
- Add unit tests for new features
- Update related documentation

### Commit Message Convention

```text
<type>(<scope>): <subject>

<body>

<footer>
```

#### **Type options**

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation update
- `style`: Code style changes
- `refactor`: Refactor
- `test`: Test related
- `chore`: Build or auxiliary tool changes

### Reporting Issues

If you find bugs or have feature suggestions, please [submit an Issue](https://github.com/comppsyunion/motion-vote/issues).

When submitting an Issue, please include:

- Detailed description of the problem
- Steps to reproduce
- Expected behavior
- Actual behavior
- System environment info

---

## 📄 License

This project is licensed under the [Apache License 2.0](LICENSE).

---

## 👥 Team

- **Project Leads**: [@buduan](https://github.com/buduan), [@hnrobert](https://github.com/hnrobert)
- **Core Developers**: See [Contributors](https://github.com/comppsyunion/motion-vote/graphs/contributors)

---

## 🙏 Acknowledgements

Thanks to all developers who contributed to this project!

Special thanks to these open source projects:

- [Vue.js](https://vuejs.org/)
- [ECharts](https://echarts.apache.org/)
- [Socket.io](https://socket.io/)

---

## 📧 Contact Us

- **Team Email**: <computerpsychounion@nottingham.edu.cn>
- **Developer Email**: Buduan <buduan461@gmail.com>; Robert He <hnrobert@qq.com>

---

## 🌟 Star History

If you find this project helpful, please give us a ⭐️ Star!

[![Star History Chart](https://api.star-history.com/svg?repos=comppsyunion/motion-vote&type=Date)](https://star-history.com/#CompPsyUnion/Motion-Vote&Date)

---

<div align="center">

Made with ❤️ by Computer Psycho Union

</div>
