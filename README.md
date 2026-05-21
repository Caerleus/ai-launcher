# AI Launcher

**A clean, local-first launcher for your AI models — LLM + Stable Diffusion — with zero cloud dependencies.**  
Everything runs on your machine. No telemetry. No subscriptions. No data leaves your device.

<p align="left">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python" />
  <img src="https://img.shields.io/badge/Flask-Backend-black?style=for-the-badge&logo=flask" />
  <img src="https://img.shields.io/badge/Local%20AI-100%25-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" />
</p>

---

### 🧭 Design Principles

- **100% local** — no cloud, no telemetry, no external calls.  
- **Zero friction** — one click to launch everything.  
- **Minimal UI** — no clutter, no distractions.  
- **Transparent** — simple `config.json`, no hidden logic.  
- **Extensible** — easy to modify, fork, or integrate.  
- **Respect hardware constraints** — designed to run even on low‑VRAM GPUs.

---


### ❓ Why AI Launcher?

Because running local AI shouldn’t require:

- memorizing command-line arguments  
- juggling multiple terminals  
- editing scripts every time you switch a model  
- dealing with complex UI frameworks  
- relying on cloud-based tools  

**AI Launcher gives you:**

- a single place to manage LLMs and Stable Diffusion  
- automatic model discovery  
- GPU selection  
- real-time status monitoring  
- an integrated prompt generator  
- a native window (PyWebView) — no browser needed  

---

### 👤 Who is this for?

- Developers using **llama.cpp** or **stable-diffusion.cpp** locally  
- Users with **low-budget GPUs** (RX 580, RX 6800, etc.)  
- People who want **full control** over their local AI stack  
- Anyone who prefers **local AI over cloud AI**  
- Tinkerers, hobbyists, and power users  

---

### ❌ Why not use LM Studio / Ollama / Fooocus?

AI Launcher is **not** a competitor.  
It’s a **minimal launcher** for people who want:

- direct control over llama.cpp and sd.cpp  
- no background services  
- no proprietary layers  
- no model management  
- no cloud dependencies  
- no forced ecosystem  

If you want a lightweight, transparent, hackable launcher — this is it.

---


### ✨ Features

| Feature | Description |
|--------|-------------|
| 🚀 **Quick Launch** | Start Chat LLM, Coding LLM and Stable Diffusion in one click |
| 🎨 **Model Selection** | Auto-detects `.gguf`, `.safetensors`, `.ckpt` |
| 🖥️ **GPU Management** | Multi-GPU Vulkan support (tested: RX 580 / RX 6800) |
| 🔗 **LoRA & VAE** | LoRA auto-loaded by sd-server; VAE selectable from UI |
| ⭐ **Image Prompt Agent** | Generates optimized SD prompts from natural language |
| ⚡ **Shortcuts** | Add links to HuggingFace, local apps, tools |
| 📊 **Real-time Status** | Port monitoring every 5 seconds |
| 💾 **Persistent Choices** | Your selections are saved between sessions |
| 🪟 **Native Window** | PyWebView — no browser required |

---

### ⚡ Quick Start

1. Download [latest release ZIP](https://github.com/Caerleus/ai-launcher/releases/latest)
2. Extract anywhere
3. Drop a `.gguf` model into `models/chat/`
4. Double-click `run_launcher.bat`
5. Done. 🚀


### 📦 Installation

```bash
# Clone the repo (replace with your fork if needed)
git clone https://github.com/Caerleus/ai-launcher.git
cd ai-launcher
pip install flask flask-cors psutil pywebview

> ⚠️ **Note on models**: AI Launcher does not include any model.
> You are responsible for downloading models you have the right to use.
> Recommended sources: [HuggingFace](https://huggingface.co), [TheBloke quants](https://huggingface.co/TheBloke).


⚙️ Configuration

All configuration lives in: 
server/config.json

Example — Chat LLM
"chat": {
  "name": "Chat LLM",
  "type": "llm",
  "exe": "../llama.cpp/llama-server.exe",
  "models_path": "../models/chat",
  "port": 5001,
  "context": 4096,
  "context_options": [512, 1024, 2048, 4096, 8192]
}

GPU Options
"gpu0":  { "label": "GPU 0",     "llm_args": "--n-gpu-layers 99 --device Vulkan0" },
"gpu1":  { "label": "GPU 1",     "llm_args": "--n-gpu-layers 99 --device Vulkan1" },
"multi": { "label": "Multi-GPU", "llm_args": "--n-gpu-layers 99 --device Vulkan0,Vulkan1" },
"cpu":   { "label": "CPU",  "llm_args": "" }

Shortcuts
{
  "id": "huggingface",
  "name": "HuggingFace",
  "type": "url",
  "url": "https://huggingface.co",
  "icon": "bi-box-seam"
}


🚀 Usage
run_launcher.bat

Option B — Terminal
cd server
python app.py

A PyWebView window opens automatically.


🎨 Image Prompt Agent

The integrated agent converts any idea (in any language) into:

Positive prompt (EN)

Negative prompt (EN)

Flow:
Your idea → Chat LLM (port 5001) → Optimized SD prompts

Requirements:

Chat LLM server must be running

Port 5001 must be free


📁 Project Structure

AI-Launcher/
├── run_launcher.bat
├── server/
│   ├── app.py
│   ├── config.json
│   ├── launcher.py
│   └── utils.py
├── models/
│   ├── chat/
│   ├── coding/
│   ├── sd/
│   ├── lora/
│   └── vae/
├── llama.cpp/
├── stable-diffusion.cpp/
└── web/
    ├── index.html
    ├── css/
    └── js/


🧱 Architecture Overview

PyWebView UI
     ↓
Flask Backend (app.py)
     ↓
launcher.py → starts/stops processes
     ↓
llama-server / sd-server

Everything is local.
No external calls.
No cloud.


🖥️ Supported Hardware

AI Launcher 1.0 is optimized for:

AMD GPUs with 4GB VRAM (RX 580, RX 570 tested)

CPU-only mode (slow but works)

Vulkan backend

Version 1.1 will target:

GPUs with higher VRAM

Larger LLMs

Faster SD inference


🔐 Privacy & Security

100% local

No cloud APIs

No telemetry

No analytics

No data collection

No external dependencies after installation

Your data stays on your machine.


🗺️ Roadmap — Version 1.1

Improved GPU handling

Better multi-GPU support

Larger model compatibility

UI refinements

Optional screenshot/GIF integration

Optional model info panel


❓ FAQ

Backend not accessible?  
Check that run_launcher.bat started Flask correctly.

No models displayed?  
Verify paths in config.json.

Image Prompt Agent not responding?  
Chat LLM must be running on port 5001.

Coding LLM not starting?  
Large models require multi-GPU.

LoRA not applied?  
LoRA is auto-loaded by sd-server from models/lora/.


⚠️ Limitations

No model downloader (by design)

No cloud integration

No automatic updates

No NVIDIA-specific optimizations (yet)

No built-in model management UI


🙏 Acknowledgements

- **[llama.cpp](https://github.com/ggml-org/llama.cpp)** — Local LLM engine
- **[stable-diffusion.cpp](https://github.com/leejet/stable-diffusion.cpp)** — Local image generation  
- **Flask** — Backend framework  
- **Bootstrap** — UI framework  
- **PyWebView** — Native desktop window  


📜 License

MIT License — see LICENSE .


## 👤 Author

[Caerleus](https://github.com/Caerleus) — Creator of AI Launcher
