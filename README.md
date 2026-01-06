# ShadowAI Ecosystem

A comprehensive voice-first AI assistant platform featuring Android app, Windows PC companion, web dashboard and Claude Code integration.

## 📱 Components

### [shadow-android](./shadow-android/)
**Primary Application** - Android app with MVVM architecture

**Features:**
- Voice-first AI assistant with hotword detection
- Multi-backend support: SSH (Claude, OpenCode, Gemini, Aider, Cursor), API (OpenAI, Anthropic, Grok), Local LLM (on-device)
- Session persistence and chat history sync across devices
- Android Auto & Wear OS companions
- Image & Video generation (SDXL, HunyuanVideo, Wan 2.1, LTX Video)
- Built-in agent system (Code writing, Debugging, Documentation, Analysis)
- Offline conversation caching
- Note-taking and task automation

**Tech Stack:**
- Kotlin, Jetpack Compose, Hilt for DI
- Room database, DataStore for preferences
- JSch for SSH connections
- Whisper.cpp for speech recognition (JNI)
- GGML/llama.cpp for local LLM (JNI)

**Build:**
```bash
cd shadow-android
./gradlew assembleDebug           # Debug APK
./gradlew bundleRelease          # Play Store AAB
./gradlew :app:installDebug    # Install to connected device
```

**Install:**
```bash
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

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
