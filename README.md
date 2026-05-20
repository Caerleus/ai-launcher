# AI Launcher

**Launch and manage your local AI models — LLM + Stable Diffusion — from a clean local interface.**  
No cloud. No subscriptions. No data sent anywhere. Ever.

[🚀 Get Started](#-installation) · [⚙️ Configuration](#️-configuration) · [❓ FAQ](#-faq)



## 🎯 Overview

**AI Launcher** is a local web interface that lets you:

- 🧠 **Start and stop** LLM servers (Chat, Coding) and Stable Diffusion
- 🎨 **Select models, LoRA, VAE and GPU** in a few clicks
- ⭐ **Generate optimized prompts** for Stable Diffusion via an integrated AI agent
- ⚡ **Access your favorite AI tools** via configurable shortcuts
- 📊 **Monitor server status** in real time

> Everything runs on your machine. No internet required after setup.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🚀 **Quick Launch** | Start Chat LLM, Coding LLM and Stable Diffusion in one click |
| 🎨 **Model Selection** | Auto-detects your local `.gguf` and `.safetensors` files |
| 🖥️ **GPU Management** | Multi-GPU support via Vulkan (tested: 2x RX 580 4GB) |
| 🔗 **LoRA & VAE** | Auto-loaded from `models/lora/` — VAE selectable from UI |
| ⭐ **Image Prompt Agent** | Write your idea in any language → AI generates an optimized SD prompt |
| ⚡ **Shortcuts** | Quick access to HuggingFace, local apps and custom URLs |
| 📊 **Real-time Status** | Port monitoring every 5 seconds |
| 💾 **Persistent Choices** | Your model and GPU selections are saved between sessions |

---

## ⚙️ Requirements

### Software

- 🐍 **Python 3.10+** — [python.org](https://python.org)
- ⚡ **llama-server** — from [llama.cpp](https://github.com/ggerganov/llama.cpp) compiled with Vulkan
- 🎨 **sd-server** — from [stable-diffusion.cpp](https://github.com/leejet/stable-diffusion.cpp)

### Python Dependencies

```bash
pip install flask flask-cors psutil pywebview

## Installation

```bash
1. Clone the repository (Not for now)
git clone https://github.com/your-username/ai-launcher.git
cd ai-launcher

2. Install dependencies
pip install flask flask-cors psutil pywebview

3. Configure server/config.json (Optional)
Adapt the paths to your machine (see ​Configuration​).
```

## Usage

4. Launch
# Option A — double-click
run_launcher.bat

# Option B — terminal
cd server
python app.py

5. Open your browser
http://127.0.0.1:5000 (Optional)
🪟 A native PyWebView window opens automatically — no browser needed.

## Features

- 📁 Project Structure
- AI-Launcher/
- ├── run_launcher.bat          ← Start here
- ├── server/
- │   ├── app.py                ← Flask backend
- │   ├── config.json           ← All configuration
- │   ├── launcher.py           ← Process manager
- │   └── utils.py              ← Utility functions
- ├── models/
- │   ├── chat/                 ← LLM Chat models (.gguf)
- │   ├── coding/               ← LLM Coding models (.gguf)
- │   ├── sd/                   ← Stable Diffusion models
- │   ├── lora/                 ← LoRA files (.safetensors)
- │   └── vae/                  ← VAE files
- ├── llama.cpp/                ← llama-server binary
- ├── stable-diffusion.cpp/     ← sd-server binary
- └── web/
- ├── index.html
- ├── css/
- └── js/

- 🔧 Configuration
- Everything is in server/config.json.
- 📦 Programs example
- "chat": {
- "name": "Chat LLM",
- "type": "llm",
- "exe": "./llama.cpp/llama-server.exe",
- "models_path": "../models/chat",
- "port": 5001,
- "context": 1024,
- "context_options": [512, 1024, 2048, 4096, 8192]
- }

- ⚠️ No default_model needed — the first model found in the folder is loaded automatically.

- 🖥️ GPU Options example
- "gpu0":  { "label": "GPU 0",     "llm_args": "--n-gpu-layers 99 --device 0" },
- "gpu1":  { "label": "GPU 1",     "llm_args": "--n-gpu-layers 99 --device 1" },
- "multi": { "label": "Multi-GPU", "llm_args": "--n-gpu-layers 99 --tensor-split 1,1" },
- "cpu":   { "label": "CPU only",  "llm_args": "--n-gpu-layers 0" }

- ⚡ Shortcuts example
- {
- "id": "huggingface",
- "name": "HuggingFace",
- "type": "url",
- "url": "https://huggingface.co",
- "icon": "bi-box-seam"
- }
- "type": "url" → opens in browser
- "type": "app" → launches a local executable

- ⭐ Image Prompt Agent
- The AI agent generates optimized Stable Diffusion prompts from a simple idea — in any language.
- Your idea (any language)
- ↓
- Chat LLM — port 5001
- ↓
- ✅ Positive prompt (EN)
- 🚫 Negative prompt (EN)

- How to use:
- Click Open Agent Prompt in the left panel
- Write your idea in any language
- Click Generate Prompt
- Copy the result directly into your SD workflow
- ⚠️ Requires Chat LLM server running on port 5001.

- 📌 Important Notes
- 🖥️ Coding LLM — Multi-GPU required for large models
- Models 6.7B+ (e.g. DeepSeek Coder 6.7B Q4_K_M) require multi-GPU to run smoothly.
- Configure "multi" in gpu_options inside config.json with the correct Vulkan args.
- Tested: 2x RX 580 4GB — Vulkan multi-GPU ✅
- 🎨 LoRA — Auto-loaded by sd-server
- LoRA files are not selected from the AI Launcher UI.
- They are automatically loaded by sd-server from the models/lora/ folder via --lora-model-dir.
- Simply place your .safetensors LoRA files in models/lora/ — no further configuration needed.
- 🎛️ VAE — Selectable from UI
- VAE files are selectable directly from the AI Launcher interface before launching Stable Diffusion.
- Place your VAE files in models/vae/.

- ❓ FAQ
- Backend not accessible?
- Check that run_launcher.bat started Flask correctly on http://127.0.0.1:5000.
- Look at the terminal window for error messages.
- No models displayed?
- Check paths in config.json — folders must exist and contain .gguf or .safetensors files.
- Image Prompt Agent not responding?
- The Chat LLM server must be ON and running on port 5001 before using the agent.
- How to add a new shortcut?
- Add an entry in "shortcuts" inside config.json and reload the page.
- Coding LLM not starting?
- Models 6.7B+ require multi-GPU. Select Multi-GPU in the GPU panel and check your Vulkan args in config.json.
- LoRA not applied to images?
- LoRA is managed automatically by sd-server. Make sure your .safetensors files are in models/lora/ before launching Stable Diffusion.

## Contributing

🙏 Acknowledgements
Project	Role
​llama.cpp​	Local LLM engine
​stable-diffusion.cpp​	Local image generation
​Flask​	Backend framework
​Bootstrap​	UI framework
​PyWebView​	Native window

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

Caerleus
