# ShadowApp 🚀✨

**The Multi-Platform Intelligence Hub for ShadowAI.**

ShadowApp is the central repository for the cross-platform ShadowAI experience, consolidating the Desktop, Mobile (Android & iOS), Web, and Refinement layers into a single ecosystem.

## 📦 Core Components

### [ShadowRefiner](./refiner) 🛡️
ShadowRefiner is our high-speed **Intent Reconstruction** and **Quality Governance** layer. It sits locally on your PC and acts as a "Chief of Staff" for all AI CLI interactions (Claude, Gemini, Codex).

*   **Intent Reconstruction:** Automatically transforms "shitty" or vague prompts into high-fidelity technical specs by analyzing your local environment context.
*   **Active Governance:** Intervenes to block zero-entropy noise and auto-triggers re-rolls for poor AI responses.
*   **Security Firewall:** Locally masks credentials and secrets before cloud transmission.

### 📱 ShadowAndroid Integration

**ShadowRefiner** is deeply integrated with the [ShadowAndroid](../shadow-android) application to provide a "Universal Controller" experience:

1.  **Distributed Notifications:** When the Refiner detects a low-quality interaction on your PC, it relays a priority alert via **ShadowBridge** directly to your Android device.
2.  **Executive Reporting:** You receive real-time "Prompt Blocked" or "Intent Improved" notifications on your phone, keeping you in control of your PC workflow even when you're away from the keyboard.
3.  **Cross-Platform Quality Loop:** The Android app serves as the dashboard for the Refiner's audit logs, allowing you to review and approve prompt reconstructions from your mobile device.

## 🛠️ Getting Started

To initialize the full ecosystem including the Refiner:

```bash
git clone --recursive https://github.com/alrightryanx/shadow-app.git
cd shadow-app
```

---
**Part of the ShadowAI Ecosystem.**

## 📱 Components

### [shadow-android](./shadow-android/)
**Primary Application** - Android app with MVVM architecture

---

### [shadow-ios](https://github.com/alrightryanx/shadow-ios) 📱
**iOS Port (Coming Soon)** - Native Swift/SwiftUI application

**Key Features:**
- Persistent SSH Roaming Engine
- Unified Sync for Projects, Notes, and Chats
- Native iOS Human Interface Design
- ShadowBridge discovery via mDNS/Bonjour

---

### [shadow-bridge](./shadow-bridge/)
**Windows PC Companion** - Python application for SSH key exchange, clipboard sync and Claude Code relay

**Features:**
- SSH key management for secure connections to Android app
- Real-time clipboard synchronization
- WebSocket server for Claude Code integration
- Web dashboard for image/video generation
- Backend communication relay

**Tech Stack:**
- Python 3.10+
- Flask web framework
- Paramiko for SSH
- WebSocket server

**Run:**
```bash
cd shadow-bridge
pip install -r requirements.txt
python shadow_bridge_gui.py              # GUI mode
python shadow_bridge_gui.py --web-server  # Web server only
```

**Configuration:**
- SSH config: `~/.ssh/` (automatically managed)
- Web dashboard: `http://localhost:19284`

---

### [backend](./backend/)
**Web Dashboard Backend** - Flask/Node.js backend for web features

**Features:**
- RESTful API for image/video generation
- WebSocket for real-time progress tracking
- PostgreSQL database for generation history
- Stable Diffusion XL local generation
- Cloud API integration (DALL-E 3, Midjourney)
- Batch processing support

**Tech Stack:**
- Flask (Python) or Express (Node.js)
- PostgreSQL
- WebSocket
- PIL (Python Imaging) or Sharp (Node.js)

**Local Development:**
```bash
cd backend
pip install -r requirements.txt              # Python
# or
npm install                                  # Node.js
python app.py                                 # Python
# or
node server.js                                # Node.js
```

**API Endpoints:**
- `POST /api/images/generate` - Generate images
- `GET /api/images/status` - Check generation status
- `POST /api/video/generate` - Generate videos
- WebSocket `/ws/progress` - Real-time updates

---

### [claude-shadow](./claude-shadow/)
**Claude Code Plugin** - Integrates ShadowAI with Claude Code

**Features:**
- Mobile notifications for Claude Code approval requests
- Session persistence sync
- Chat history relay to Android app
- Two-way communication between Claude Code and ShadowAI

**Installation:**
```bash
cd claude-shadow
npm install
```

**Configuration:**
- Plugin manifest: `.claude-plugin/plugin.json`
- Version control for updates
- Session state management

**Use with Claude Code:**
1. Open Claude Code project
2. Install plugin from local path
3. Configure ShadowAI connection
4. Approve/deny requests from Android app

---

### [gemini-shadow](./gemini-shadow/)
**Gemini Bridge Relay** - Proxy for Gemini API access

**Features:**
- HTTPS relay for Gemini API calls
- Request/response streaming
- Error handling and retry logic
- Rate limiting support

**Tech Stack:**
- Node.js
- Express.js
- Axios for HTTP

**Run:**
```bash
cd gemini-shadow
npm install
npm start
```

**Configuration:**
- Environment variables for API keys
- Proxy settings
- CORS configuration

---

## 🛠️ Setup & Configuration

### Android App

1. **Install APK:**
   ```bash
   adb install -r shadow-android/app/build/outputs/apk/debug/app-debug.apk
   ```

2. **Initial Setup:**
   - Open app
   - Grant microphone and storage permissions
   - Configure AI backend (SSH, API, or Local LLM)

3. **SSH Backend Setup:**
   - Configure SSH host, username, authentication
   - Select CLI provider (Claude, OpenCode, Gemini, Aider, Cursor)
   - Test connection

4. **API Backend Setup:**
   - Enter API keys (OpenAI, Anthropic, Grok)
   - Configure model selection
   - Test connection

### ShadowBridge (PC)

1. **Install Dependencies:**
   ```bash
   cd shadow-bridge
   pip install -r requirements.txt
   ```

2. **Run:**
   ```bash
   python shadow_bridge_gui.py
   ```

3. **Web Dashboard Access:**
   - Open `http://localhost:19284` in browser
   - Configure image/video generation settings

### Claude Code Plugin

1. **Install:**
   ```bash
   cd claude-shadow
   npm install
   ```

2. **Configure in Claude Code:**
   - Settings → Plugins → Add Local Plugin
   - Select `claude-shadow` directory
   - Configure ShadowAI webhook URL

### Gemini Bridge

1. **Install:**
   ```bash
   cd gemini-shadow
   npm install
   npm start
   ```

2. **Configure:**
   - Set `GEMINI_API_KEY` environment variable
   - Configure proxy settings if needed

---

## 🌐 Network Architecture

```
┌─────────────────┐         ┌──────────────────┐
│  Android App    │◄─────►│  ShadowBridge    │
│  (shadow-       │ SSH    │  (Windows PC)    │
│   android)       │         │                  │
└────────┬────────┘         └────────┬─────────┘
         │                          │
         │ WebSocket                │ HTTP/WS
         │                          │
         ▼                          ▼
┌─────────────────┐         ┌──────────────────┐
│  Claude Code    │◄─────►│  ShadowWeb       │
│  (claude-       │ Plugin │  (backend)        │
│   shadow)       │         │                  │
└─────────────────┘         └──────────────────┘
                                      │
                                      │ API
                                      ▼
                               ┌──────────────┐
                               │  Gemini API   │
                               │  (OpenAI,    │
                               │   Anthropic)  │
                               └──────────────┘
```

---

## 📁 Project Structure

```
shadow-app/
├── shadow-android/          # Android app (primary)
│   ├── app/                # Main app module
│   ├── wear/               # Wear OS app
│   └── shared/             # Core business logic
├── shadow-bridge/          # Windows PC companion
│   ├── plugins/             # Claude Code plugin
│   └── web/                # Web dashboard
├── backend/                # Web backend APIs
│   ├── routes/             # API endpoints
│   ├── scripts/            # Generation scripts
│   └── database/           # Schema
├── claude-shadow/           # Claude Code plugin
├── gemini-shadow/           # Gemini relay
└── README.md               # This file
```

---

## 🔐 Security & Privacy

### SSH Key Management
- Keys stored in `~/.shadowai/` (encrypted)
- Public key automatically distributed to Android
- Private key never leaves PC

### API Keys
- Encrypted storage on Android (AES-256-GCM)
- Encrypted storage on PC (AES-256-GCM)
- Keys never transmitted to ShadowAI servers

### Data Persistence
- Session history stored locally
- Encrypted database for sensitive data
- No cloud analytics or telemetry

---

## 🚀 Building from Source

### Android App

**Prerequisites:**
- Android Studio Hedgehog or newer
- JDK 17+
- Android SDK 34+

**Build:**
```bash
cd shadow-android
./gradlew clean
./gradlew assembleDebug
```

**Sign:**
- Keystore: `keystore.properties` (local dev only)
- Release: Follow Android app signing guide

### ShadowBridge

**Prerequisites:**
- Python 3.10+
- Windows 10+

**Build:**
```bash
cd shadow-bridge
pip install -r requirements.txt
```

### Web Backend

**Prerequisites:**
- 
