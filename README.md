# LLLM - Local Large Language Model

**LLLM** is an open-source AI platform that supports local and remote Large Language Models across Windows, Linux, macOS, and Android/Termux environments.

The project is open source and uses the MIT license.

## Purpose

LLLM is a local and remote LLM platform usable on Windows, Linux, macOS, and Android/Termux.

The project will be open source and use the MIT license.

## Model Engines

- **llama.cpp**: Primary local inference engine.
- **GGUF**: Local model format.
- **OpenRouter**: External model API provider.
- **NVIDIA NIM**: External model API provider.
- **Custom Python runner**: "runner.py".

Ollama is not required.

## CLI Command System

The following commands are developed as fully working features:

- `lllm run`
- `lllm terminal`
- `lllm terminal -orkey -local false`
- `lllm terminal -nimkey -local false`
- `lllm new models`
- `lllm new assets`
- `lllm new skills`
- `lllm new folder`
- `lllm skills list`
- `lllm skills create NAME`
- `lllm skills delete NAME`
- `lllm ports login 4000`

### Command Responsibilities

- **"lllm run"**: Starts the local API and web server.
- **"lllm terminal"**: Opens an AI chat via the terminal.
- **"-orkey"**: Uses OpenRouter API.
- **"-nimkey"**: Uses NVIDIA NIM API.
- **"-local false"**: Uses the selected remote provider instead of local inference.
- **"lllm new models"**: Opens the GGUF model download and management system.
- **"lllm new assets"**: Converts the Assets folder into a ZIP archive.
- **"lllm new skills"**: Prepares the Skills directory and management system.
- **"lllm skills"**: Performs skill listing, creation, and deletion operations.
- **"lllm ports login 4000"**: Connects to the LLLM service on the specified port.

## Project Folder Structure

```
LLLM/
├── runner.py
├── lllm
├── index.html
├── models/
├── assets/
├── skills/
├── config/
├── api/
├── core/
├── downloads/
├── logs/
├── README.md
├── LICENSE
└── .gitignore
```

## Web UI

A modern, professional, and mobile-responsive AI chat interface is developed.

Features:

- Model selection.
- Local and remote provider selection.
- Chat history.
- New chat.
- Markdown and code blocks.
- Streaming responses.
- Model download/management screen.
- Skills management screen.
- API connection status.
- Settings and system prompt.

## Technical Requirements

- Python backend.
- llama-cpp-python.
- llama.cpp.
- GGUF models.
- OpenRouter API.
- NVIDIA NIM API.
- HTML, CSS and JavaScript frontend.
- OpenAI compatible API structure.
- Do not write API keys into the source code or frontend. Use secure configuration files and environment variables.

## Development Rules

1. Do not produce only example or fake code; develop working features.
2. Add new features without breaking existing ones.
3. Test every new feature.
4. Specify errors and missing dependencies.
5. Keep the README.md file updated.
6. Avoid unnecessary dependencies.
7. Do not add large model files to the Git repository.
8. Deliver updated project files at every stage.
9. Check Android and Termux compatibility separately.
10. Observe licenses and API usage terms.

## Goal

Transform LLLM into an independent open-source AI platform with its own terminal commands, custom Python runner, model manager, API integrations, and advanced chat interface, capable of running real models.

First, examine the existing source code, then detect missing features and begin development.

## Target

Transform LLLM into a standalone open-source AI platform that can run real models, with its own terminal commands, custom Python runner, model manager, API integrations, and advanced chat interface.

## Installation

See `/root/outputs/installation.md` for detailed installation instructions.

## Installation (Quick Start)

```bash
# 1. Install
dpkg -i /root/lllmbeta_1.0.0_all.deb

# 2. Start server
lllm run

# 3. Open chat
# Browser: http://localhost:4000
# CLI: lllm terminal

# 3. Use skills
lllm skills list
lllm skills create NAME
lllm skills delete NAME
```

## License

This project is licensed under the MIT License. See the LICENSE file for details.

## Contact

For issues, contributions, or questions, please refer to the project repository or open an issue.

---
*This README is generated for the LLLM project. Last updated: November 2026.*