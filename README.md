# ShadowAI - The Ultimate AI Coding Companion

[![Get it on Google Play](https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png)](https://play.google.com/store/apps/details?id=com.shadowai.release)

ShadowAI is a production-ready ecosystem designed for seamless AI orchestration between mobile devices and desktop environments. It bridges your phone to your PC's terminal, enabling a hands-free, voice-first coding and automation experience.

## 🌐 The Ecosystem

1.  **[shadow-android](https://github.com/alrightryanx/shadow-android) (Android App)**: The mobile core. A voice-first AI assistant supporting Android, Android Auto, Wear OS, and Google TV. It serves as your primary interface for hands-free AI interaction.
2.  **[shadow-bridge](https://github.com/alrightryanx/shadow-bridge) (Windows PC Companion)**: The infrastructure bridge. This Windows application connects your phone to your PC, enabling ADB execution, SFTP transfers, and local tool orchestration.
3.  **[shadow-web](https://github.com/alrightryanx/shadow-web) (Orchestration Backend)**: The central brain. A high-performance backend managing cloud integrations, usage tracking, unified memory, and multi-agent team coordination.
4.  **[claude-shadow](https://github.com/alrightryanx/claude-shadow) (Claude Code Plugin)**: The developer's relay. A specialized plugin for Anthropic's Claude Code that enables mobile notifications and remote approvals.
5.  **[gemini-shadow](https://github.com/alrightryanx/gemini-shadow) (Gemini Bridge Relay)**: The developer's relay. A specialized plugin for Google's Gemini CLI that enables mobile notifications and remote approvals.

---

## 🚀 Vision
ShadowAI moves beyond simple chatbots. Our platform is built for advanced cross-platform automation:

- AI agents on your PC can build software projects and automatically push or install assets on your phone via ADB or SFTP.
- Zero-latency interaction with haptic feedback and noise gating makes the AI as responsive as a physical button.
- A "Stability First" mandate ensures data integrity through explicit migrations and AEAD encryption for all persistent data.

## 🛠️ Key Technical Pillars
- The system intelligently switches between local LLMs, cloud APIs, and remote SSH backends based on task requirements.
- The platform uses atomic file writes and end-to-end encryption to protect orchestration logs and sensitive user data.
- Native Android Auto support and persistent background services enable seamless "Always-On" voice control.

## 📁 Project Structure
- `shadow-android/`: Main Android application source.
- `shadow-bridge/`: Windows desktop companion and web dashboard.
- `backend/`: The `shadow-web` server infrastructure.
- `claude-shadow/` & `gemini-shadow/`: Platform-specific plugin implementations.
- `docs/`: Design documents, stability audits, and benchmark reports.

---
© 2026 ShadowAI. All rights reserved.
