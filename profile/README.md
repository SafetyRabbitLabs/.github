# 🐇 SafetyRabbitLabs

Welcome to **SafetyRabbitLabs**! This is the core development hub for the **VISION** ecosystem—an enterprise-grade secure workspace and AI-governed exam governance platform.

---

## 🛠️ Active Repositories

### 1. 🎓 [Vision-Browser](https://github.com/SafetyRabbitLabs/Vision-Browser)
A hardened Chromium-based desktop runtime designed to lock down the operating system and prevent unauthorized actions during high-stakes assessments.
* **Technology**: C# / .NET (WPF Shell) + CEF (Chromium Embedded Framework) + CefSharp.
* **Key Features**:
  * Prevents OS-level shortcuts (Alt+Tab, Alt+F4, Win Key, etc.).
  * Blocks screenshot captures and screen-recording attempts.
  * Disables DevTools, right-click context menus, and extensions.
  * Continuously monitors running background processes to block blacklisted applications.

### 2. 📝 [Ai-secure-exam-browser](https://github.com/SafetyRabbitLabs/Ai-secure-exam-browser) *(OJT Project)*
The core enterprise web application platform that powers the examinations, real-time proctoring, and automated evaluation.
* **Technology**: Node.js, Express, MongoDB, Redis, BullMQ, Socket.IO, React.
* **Key Features**:
  * **Input Governance**: Zod strict payload validation to prevent mass-assignment.
  * **Asynchronous Grading**: Redis and BullMQ powered grading workers (using Judge0 / isolated-vm).
  * **Real-time Proctoring**: Socket.IO for real-time tracking, live monitoring, and snapshot vaults.
  * **Hardened Auth**: Session versioning, JWT rotation, and proactive theft detection.

---

## 🔒 Security & Privacy Notice
All repositories in this organization are kept **Private** to protect proprietary core logic, custom security layers, and exam integrity enforcement mechanisms.

*For installation, setup instructions, or API documentation, please refer to the respective repository directories.*
