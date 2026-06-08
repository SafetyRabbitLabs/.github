# 🐇 SafetyRabbitLabs

Welcome to **SafetyRabbitLabs**! This is the central engineering hub for the **VISION** ecosystem—an enterprise-grade secure workspace and AI-governed assessment runtime platform.

The VISION ecosystem provides high-integrity online evaluations, secure interviewing workspaces, and absolute device lockdown by combining native OS-level security layers with real-time AI-proctoring pipelines.

---

## 🛠️ Ecosystem Architecture & Repositories

### 1. 🎓 [Vision-Browser](https://github.com/SafetyRabbitLabs/Vision-Browser)
A hardened Chromium-based desktop runtime designed to lock down the operating system and enforce complete integrity during assessments. Rather than acting as a simple exam browser, it serves as a reusable **Secure Workspace Runtime** designed to host multiple child products (VISION Exam, VISION Interview, VISION Certification, and Enterprise Lockdown).

* **Technology Stack**: C# / .NET (WPF Native Shell) + CEF (Chromium Embedded Framework) + CefSharp Bindings + Windows API Interop (P/Invoke).
* **Core Security & OS Lockdown Mechanisms**:
  * **Low-Level Input Hooks**: Uses native keyboard hooks (`SetWindowsHookEx` via `user32.dll`) to block OS-level navigation shortcuts including `Alt+Tab`, `Alt+F4`, `Windows Key`, `Ctrl+Esc`, and task-switching.
  * **Anti-Screen Capture (DRM)**: Employs Windows Display Affinity API (`WDA_EXCLUDEFROMCAPTURE`) to black out the browser window in all screenshots, video capture tools, screen sharing platforms, and remote desktop streams.
  * **Process Governance Engine**: Actively monitors running system processes via WMI and background polling to detect, alert, or force-terminate unauthorized software (e.g., Discord, TeamViewer, AnyDesk, Virtual Machines).
  * **Hardened CEF Runtime**: Customized Chromium settings to block developer tools (DevTools), hide address/status bars, restrict extensions, prevent right-click context menus, and intercept all popup/multi-monitor windows.
  * **Policy-Driven Execution**: Behaviors, URL whitelists, and restriction strictness are dynamically injected per session via the admin portal policy engine.

---

### 2. 📝 [Ai-secure-exam-browser](https://github.com/SafetyRabbitLabs/Ai-secure-exam-browser)
The core web application platform and scalable backend orchestrating assessments, real-time proctoring data streams, and automated evaluation engines.

* **Technology Stack**: Node.js, Express, MongoDB (Mongoose), Redis, BullMQ, Socket.IO, React, Zod.
* **Core Capabilities & Engineering Standards**:
  * **Input Governance Layer (Zod)**: All incoming payloads are strictly validated using Zod schemas. Strict mode is enforced to reject extra fields and systematically prevent mass-assignment vulnerabilities.
  * **Asynchronous Grading Pipeline**: Offloads code evaluation to background workers powered by Redis and BullMQ. Grading jobs are isolated and executed securely using sandboxed runtimes (Judge0 API & JSDOM/isolated-vm).
  * **Real-Time Proctoring & Event Streams**: Establishes JWT-authenticated Socket.IO connections for continuous state syncing, live event logs (tab switches, webcam violations), and live camera snapshot archiving to Cloudinary.
  * **Hardened Session & Token Security**:
    * *Refresh Token Rotation (RTR)*: Every token refresh cycle generates a rotating token; any attempt to reuse an old token triggers proactive account lockdown (Theft Detection).
    * *Session Versioning*: JWTs contain a `sessionVersion` identifier. Incrementing this version in the database acts as a global kill switch, immediately invalidating all active socket connections and tokens.
  * **Centralized Bootstrap Orchestration**: Employs a linear startup sequence (`Environment Checks` ➡️ `DB Connect` ➡️ `Redis Connect` ➡️ `Worker Registry` ➡️ `Cache Warmup` ➡️ `Server Listen` ➡️ `Health Monitor`).

---

## 🔒 Security & Privacy Notice
All repositories in this organization are kept **Private** to safeguard proprietary security measures, sandbox escape preventions, anti-cheat mechanisms, and client assessment data.

*For setup guides, local configuration (.env keys), or API documentation, please refer to the respective repository directories.*
