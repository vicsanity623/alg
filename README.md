<div align="center">

# 🛠️ S•IDE
**The Zero-Config, Sandbox-IDE (PWA) Browser Workstation**

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)]()
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)]()
[![PWA Ready](https://img.shields.io/badge/PWA-Ready-8A2BE2?style=for-the-badge&logo=pwa&logoColor=white)]()
[![CodeMirror](https://img.shields.io/badge/CodeMirror-5.65-blue?style=for-the-badge)]()
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-0-success?style=for-the-badge)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

A lightweight, fully functional Web IDE contained entirely within the browser. Write code, manage virtual files, compile Markdown, and preview your web applications with a built-in proxied developer console—all without starting a local server. Fully mobile-responsive and installable natively on your device.

[Features](#-features) • [Quick Start](#-quick-start) • [How to Use](#%EF%B8%8F-how-to-use) • [Under the Hood](#-under-the-hood) • [Contributing](#-contributing)

</div>

---

## ⚡ Features

- **📦 Zero-Server Architecture**: Runs purely in the browser. No Node.js, no Webpack, no local servers required.
- **📱 PWA & Offline Support**: Installable natively on iOS, Android, and Desktop. Service Workers ensure the IDE functions **100% offline**.
- **💾 Auto-Save Persistence**: Every keystroke is saved to `localStorage`. Never lose your work to an accidental refresh.
- **🗂️ Virtual File System**: Create, edit, and link multiple HTML, CSS, and JS files just like a real local project.
- **🔄 On-the-Fly Bundler**: Automatically intercepts `<script src="...">` and `<link href="...">` tags and injects your virtual files dynamically before rendering.
- **🖥️ Integrated Smart Console**: Intercepts standard `console.log` calls from the preview and displays them in the IDE. Includes custom serialization for complex DOM elements (like `<canvas>`) and Web APIs.
- **📦 Drag, Drop & Export**: Drag local files directly into the browser to import them, and export your entire workspace as a `.zip` archive.
- **📝 Markdown Compilation**: Natively converts and previews `.md` files instantly.
- **🎨 SOTA Editor Experience**: Powered by CodeMirror (Dracula theme) with syntax highlighting, line numbers, and a dedicated **⇥ TAB button** tailored for mobile touch-keyboards.

---

## 🚀 Quick Start

Because SandboxIDE is completely standalone, setup takes seconds:

### Desktop
1. **Host** or open the `index.html` file in any modern browser (Chrome, Firefox, Safari, Edge).
2. Start coding immediately.
3. *Optional:* Click the install icon in your browser's address bar to install it as a standalone Desktop App.

### Mobile (iOS / Android)
1. Navigate to the hosted URL on your device.
2. Tap **"Share"** (iOS) or **"Menu"** (Android) and select **"Add to Home Screen"**.
3. Launch SandboxIDE from your home screen for a full-screen, native-app experience!

---

## 🕹️ How to Use

### 1. Managing Files
On the left-hand side (or the top swipeable bar on mobile) is your **File Explorer**.
- Click the **`+`** button to create a new file (e.g., `style.css` or `app.js`).
- Drag and drop existing `.js`, `.html`, `.css`, or `.md` files into the window to import them.
- Click the **`↺`** button to reset the environment to the default boilerplate.

### 2. Linking Files Together
SandboxIDE acts exactly like a real web server. You can link the files you create in your virtual file system directly inside your `index.html` file.

**Example `index.html`:**
```html
<!DOCTYPE html>
<html>
<head>
    <!-- SandboxIDE will bundle this automatically! -->
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <canvas id="game"></canvas>
    
    <!-- SandboxIDE will bundle this automatically! -->
    <script src="index.js"></script>
</body>
</html>
```

### 3. Using the Interactive Console
Unlike standard iframes that hide logs in your browser's F12 dev tools, SandboxIDE features a built-in console panel that accurately serializes Complex Objects.

**Example `index.js`:**
```javascript
const game = document.getElementById("game");
console.log("Canvas Element:", game); // Outputs actual <canvas id="game"> element!

const ctx = game.getContext("2d");
console.log("Canvas Context:", ctx); // Natively serialized, prevents "[object Object]"
```

### 4. Running & Exporting
- Hit the **`▶ Run`** button to parse your HTML, inject your local scripts/styles, and render the Live Preview.
- Hit the **`📦 Export ZIP`** button to bundle your entire virtual file system into a `.zip` file for external deployment.

---

## 🧠 Under the Hood

Curious how a multi-file IDE works entirely client-side? Here is the magic:

<details>
<summary><strong>1. The Virtual File System & Auto-Save</strong></summary>
<br>
All files are stored in a JavaScript Dictionary object (`const files = {}`) and synced instantly to the browser's <code>localStorage</code>. When you switch tabs, CodeMirror's value is dynamically swapped and persisted.
</details>

<details>
<summary><strong>2. RegEx Bundling</strong></summary>
<br>
When you click Run, the app uses Regular Expressions to parse your HTML string. It looks for <code>&lt;script src="[filename]"&gt;&lt;/script&gt;</code>. If <code>[filename]</code> exists in the VFS dictionary, it replaces the network request with an inline script containing your exact code.
</details>

<details>
<summary><strong>3. Iframe Console Proxying</strong></summary>
<br>
Before injecting the code into the <code>&lt;iframe&gt;</code> via <code>srcdoc</code>, SandboxIDE prepends an Interceptor Script. This script hijacks <code>console.log</code>, <code>warn</code>, <code>error</code>, and <code>window.onerror</code>. It intercepts the arguments, serializes them, and uses <code>window.parent.postMessage</code> to securely send the data back to the main IDE UI.
</details>

---

## 🛣️ Roadmap

- [x] Virtual File System creation
- [x] Syntax Highlighting via CodeMirror
- [x] Iframe Live Preview & Smart Console
- [x] Mobile Responsiveness & PWA implementation
- [x] Auto-save to `localStorage`
- [x] Drag-and-drop file imports
- [x] Support for Markdown rendering
- [x] Export project as a `.zip` file
- [ ] Add Prettier code auto-formatting integration
- [ ] GitHub Gist Import/Export capabilities
- [ ] Multiple UI/Editor Themes

---

## 🤝 Contributing

Contributions make the open-source community an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.

---

<div align="center">
  <b>Built with ❤️ for rapid, offline, browser-based prototyping.</b>
</div>
