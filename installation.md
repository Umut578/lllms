# LLLM - Kurulum ve Kullanım Kılavubu

**LLLM** (Local Large Language Model), Windows, Linux, macOS ve Android/Termux ortamlarında çalışabilen, yerel ve uzaktaki LLM modellerini destekleyen bir açık kaynaklı AI platformudur. MIT lisansı altında dağıtılır.

---

## ✨ Özellikler

- **Çoklu Model Motoru**:
  - Yerel: `llama.cpp` tabanlı inference (GPU/CPU)
  - Uzak: OpenRouter API, NVIDIA NIM API
- **CLI Komut Seti**: 15+ komut ile tam kontrol
- **Web Arayüzü**: Modern, Bootstrap + AJAX, streaming yanıtlar
- **Skills Sistemi**: Python modülleri ile genişletilebilir
- **Platform Desteği**: Windows, Linux, macOS, Android/Termux

---

## 📦 1. Sistem Gereksinimleri

### Donanım
- **Yerel inference** için: GPU (NVIDIA kartı önerilir) veya modern CPU
- **Bellek**: Model boyutuna bağlı (4GB-Q4'ten 24GB-Q5'e kadar)
- **Depolama**: GGUF modeller için 10GB+ boş alan

### Yazılım
- Python 3.10+
- `python3-yaml`, `python3-flask`, `python3-requests` paketleri
- (İsteğe bağlı) `llama-cpp-python` yerel inference için

### Ortam
- **Linux/macOS**: `bash` ile çalıştırılabilir
- **Windows**: PowerShell veya WSL2
- **Termux**: `pkg install python3` + pip paketler

---

## 🛠️ 2. İnstallasyon (Kurulum)

### Seçenek 1: `dpkg` ile Sistem-Wide Kurulum (Önerilen)

```bash
# 1. Debian paketi indirin/oluşturun
dpkg -i /root/lllmbeta_1.0.0_all.deb

# 2. Komutun erişilebilir olduğunu kontrol edin
which lllm

# 3. Kullanım başlatın
lllm
```

### Seçenek 2: Manuel Python ile Çalıştırma

```bash
# 1. LLLM dizinine gidin
cd /root/LLLM

# 2. Bağımlılıkları yükleyin
pip3 install -r requirements.txt

# 3. Komutları test edin
lllm --help
# veya
python3 runner.py --help
```

### Seçenek 3: Virtual Environment ile

```bash
# 1. Virtual environment oluşturun
python3 -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# 2. Bağımlılıkları yükleyin
pip install -r /root/LLLM/requirements.txt

# 3. Runner'ı çalıştırın
python3 /root/LLLM/runner.py
```

---

## 💻 3. `lllm` Komut Arayüzü

### Temel Komutlar

| Komut | Açıklama | Örnek |
|-------|----------|-------|
| `lllm run` | Yerel API ve web sunucusunu başlatır | `lllm run` |
| `lllm terminal` | Terminal üzerinden AI sohbeti açar | `lllm terminal` |
| `lllm help` | Kullanılabilir komutları listeler | `lllm help` |

### `run` Komutu

```bash
# Temel kullanım
lllm run

# Debug modu
lllm run --debug

# Çıktı: 
# 🚀 LLLM web sunucusu başlatılıyor
# Tarayıcıda http://localhost:4000 adresine gidin
```

### `terminal` Komutu

```bash
# Yerel inference (llama.cpp motoru)
lllm terminal

# OpenRouter API ile
lllm terminal -orkey

# NVIDIA NIM API ile
lllm terminal -nimkey

# Yerelsiz (uzak) kullanım
lllm terminal -local false

# Çıktı: 💬 Terminal sohbeti açıldı...
```

### `new` Komutları

```bash
# Models listele
lllm new models

# Assets'i ZIP'e dönüştür
lllm new assets

# Skills dizinini hazırla
lllm new skills

# Yeni klasör oluştur
lllm new folder test_folder
```

### `skills` Komutları

```bash
# Skill'leri listele
lllm skills list

# Yeni skill oluştur
lllm skills create metin_analizi

# Skill sil
lllm skills delete metin_analizi
```

### `ports` Komutu

```bash
# Port bağlantısı kontrolü
lllm ports login 4000

# Çıktı: WARNING:root:Port 4000 açıkta: 111
# (111 = port erişilebilir, 0 = hizmet çalışıyor)
```

---

## 🌐 4. Web Arayüzü Kullanımı

### Yerel Sunucu ile

```bash
# Sunucuyu başlatın
lllm run

# Tarayıcıda açın:
# http://localhost:4000/web
# veya sadece: http://localhost:4000
```

### Arayüz Özellikleri

- **Model Seçimi**: Yerel / OpenRouter / NVIDIA NIM
- **Sağlayıcı Değişimi**: Butonlar ile hızlı geçiş
- **Sohbet Geçmişi**: Otomatik kaydedilir
- **Markdown Destek**: **Bold**, *İtalik*, `code`, ```code blokları```
- **Streaming Yanıtlar**: Token token görünür
- **Yeni Sohbet**: Başlangıçta temizle
- **Ayarlar**: Provider ve model değiştirilebilir

---

## ⚙️ 5. Yapılandırma (Configuration)

### `config/config.yaml` Dosyası

```yaml
app:
  name: "LLLM"
  version: "1.0.0"
  host: "0.0.0.0"
  port: 4000
  debug: false

model:
  default_provider: "local"
  providers: ["local", "openrouter", "nim"]
  models_dir: "models"
  context_length: 4096
  n_gpu_layers: 0        # GPU katmanları (0 = CPU sadece)
  n_threads: 4           # CPU threaded sayısı
  temperature: 0.7
  top_p: 0.9
  max_tokens: 2048

openrouter:
  enabled: true
  base_url: "https://openrouter.ai/api/v1"
  model: "openrouter/auto"
  api_key: "${OPENROUTER_API_KEY}"

nim:
  enabled: true
  base_url: "https://integrate.api.nvidia.com/v1"
  model: "meta/llama-3.1-8b-instruct"
  api_key: "${NVIDIA_API_KEY}"

local:
  engine: "llama.cpp"
  runner: "runner.py"
  gguf_path: "models"
  default_model: ""
  n_ctx: 4096
```

### `.env.example` - API Anahtarları

```env
# LLLM API Anahtarları
# Bu dosyayı kopyalayın ve değerleri doldun:
# .env (git'e commit edilmeyecek - .gitignore ile)

OPENROUTER_API_KEY="sk-or-xxxx"
NVIDIA_API_KEY="nvapi-xxxx"
```

### API Anahtarları Güvenliği
- **Asla** kaynak koduna (frontend/source) yazmayın
- `.env` dosyası `.gitignore` ile korunur
- Değişkenler `os.environ` veya YAML ile yapılandırılır
- Production'da secret yönetimi (Vault/Secret Manager) önerilir

---

## 📱 6. Platform Bağımlı Uygulama

### Linux (Debian/Ubuntu)

```bash
# Bağımlılıklar
sudo apt-get update
sudo apt-get install -y python3-pip python3-yaml

# Paket kur
dpkg -i /root/lllmbeta_1.0.0_all.deb

# Çalıştır
lllm run
```

### macOS

```bash
# Homebrew ile
brew install python3

# Pip ile
pip3 install -r /root/LLLM/requirements.txt

# Çalıştır
cd /root/LLLM && llm run
```

### Windows

```powershell
# PowerShell
cd C:\LLLM
python3 -m pip install -r requirements.txt
.\..\..\root\lllm\lllm run
```

### Android / Termux

```bash
# Termux'ta
pkg update && pkg install python3 git
pip3 install -r /root/LLLM/requirements.txt

# Çalıştır
cd /root/LLLM
lllm run
```

Not: Termux'ta yerel inference (`llama-cpp-python`) kurulumu ek adımlar gerektirebilir.

---

## 🔧 7. Sorun Giderme (Troubleshooting)

### Yaygın Hatalar

| Hata | Neden | Çözüm |
|------|-------|-------|
| `ModuleNotFoundError: No module named 'yaml'` | PyYAML eksik | `pip3 install pyyaml` |
| `ModuleNotFoundError: No module named 'flask'` | Flask eksik | `pip3 install flask` |
| `ModuleNotFoundError: No module named 'requests'` | Requests eksik | `pip3 install requests` |
| `llama-cpp-python yüklü değil` | Yerel motor yok | `pip3 install llama-cpp-python` ya da GPU kullanın |
| `Port 4000 açıkta: 111` | Sunucu çalışıyor | `lllm run` komutundan tekrar başlayın |
| `API anahtarı bulunamadı` | `.env` eksik | `.env.example` kopyalayın ve doldurun |
| `Model dosyası bulunamadı` | GGUF yok | `lllm new models` veya modelleri `models/` klasörüne koyun |

### Logları Kontrol Et

```bash
# Log dosyası
cat /root/LLLM/logs/lllm.log

# Canlı çıktı
lllm run 2>&1 | tail -20
```

---

## 📊 8. Destek ve Kaynaklar

### İletişim
- Proje: `/root/LLLM`
- Dokümantasyon: `README.md`
- Hatalar: Issue açın ya da `lllm help` ile yardım

### Lisans
```
MIT License

Copyright (c) 2026 LLLM Project

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions...

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

### Kaynakça
- [LLLM GitHub Repository](https://github.com/lllm-project/lllm)
- [llama.cpp Documentation](https://github.com/ggerganov/llama.cpp)
- [OpenRouter API Docs](https://openrouter.ai/docs)
- [NVIDIA NIM Docs](https://docs.nvidia.com/nim)

---

## 🚀 Hızlı Başlangıç (Quick Start)

```bash
# 1. Kur
dpkg -i /root/lllmbeta_1.0.0_all.deb

# 2. API anahtarları (isteğe bağlı)
cp /root/LLLM/.env.example /root/LLLM/.env
# .env dosyasını düzenleyin

# 3. Sunucuyu başlatın
lllm run

# 4. Tarayıcıda açın
# http://localhost:4000

# 5. Sohbete başlayın
lllm terminal
# ya da tarayıcı üzerinden sohbet edin
```

---
*Bu belge LLLM projesi için oluşturulmuştur. Son güncelleme: November 2026*