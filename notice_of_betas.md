# Beta Notice for LLLM

**NOTICE: Beta Software**

This software is currently in beta. While extensively tested, please be aware of the following:

- **Features may change** between versions as the project evolves.
- **Known issues** are documented in the issue tracker.
- **Performance varies** based on hardware and model selection.
- **Beta versions are not covered** by the standard support policy.

## What's New in This Beta

- **Multi-provider support**: Local (llama.cpp), OpenRouter, and NVIDIA NIM APIs.
- **CLI command system** with 15+ fully working commands.
- **Modern web UI** with Markdown support, streaming responses, and model selection.
- **Skills system** for extensible plugins.
- **Cross-platform compatibility** (Windows, Linux, macOS, Android/Termux).

## Installation

```bash
# Debian package
dpkg -i /root/lllmbeta_1.0.0_all.deb

# Or from source
cd /root/LLLM
pip install -r requirements.txt
```

## Usage

```bash
# Start the server
lllm run

# Open terminal chat
lllm terminal

# Or access via browser
# http://localhost:4000
```

## Feedback

Please report bugs and feature requests via the issue tracker. 
Beta testers are encouraged to test new features and provide feedback.

## License

This project is licensed under the MIT License. See LICENSE for details.

---
*Beta notice generated for LLLM project. Last updated: November 2026.*