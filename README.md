# 🎵 Lackadaisical Codex Extractor

**Production-Grade Audio Analysis & Linguistic Processing System**

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/lackadaisical-security/codex-extractor)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE.md)
[![Python](https://img.shields.io/badge/python-3.11+-brightgreen.svg)](https://python.org)
[![Security](https://img.shields.io/badge/security-enterprise%20grade-red.svg)](#security-features)

> *Zero mock/simulated/placeholder code - All real functionality*

© **Lackadaisical Security 2025** · [https://lackadaisical-security.com](https://lackadaisical-security.com)

---

## 🎯 Overview

The Lackadaisical Codex Extractor is a comprehensive multi-modal analysis system that combines advanced audio processing, speech recognition, acoustic analysis, natural language processing, and secure data export capabilities. Built with production-grade security and stunning 80s retro cosmic web interface.

### ✨ Key Features

- **🎵 Advanced Audio Processing**: Multi-format support with FFmpeg integration
- **🎤 High-Accuracy Speech Recognition**: Whisper ASR with confidence scoring
- **🔊 Acoustic Feature Extraction**: YIN pitch, MFCC, formant analysis
- **🧠 Natural Language Processing**: spaCy pipeline with semantic embeddings
- **⚡ Feature Alignment**: Word/syllable/phoneme-level temporal synchronization
- **📊 Schema-Validated Export**: AI-optimized JSON with quality metrics
- **🛡️ Enterprise Security**: JWT auth, AES-GCM encryption, audit logging
- **🌌 Cosmic Web Interface**: 80s retro theme with live API monitoring
- **⚙️ Professional CLI**: Rich formatting with batch processing
- **🚀 REST API**: FastAPI server with async background processing

---

## 🚀 Quick Start

### Prerequisites

- **Python 3.11+** (64-bit)
- **FFmpeg** (included in project)
- **4GB+ RAM** recommended
- **Windows 10/11** (primary target)

### Installation

```powershell
# Clone or extract project
cd Lackadaisical-Codex-Extractor

# Create virtual environment
python -m venv .venv
.venv\Scripts\Activate.ps1

# Install dependencies
pip install -r requirements.txt

# Download spaCy model
python -m spacy download en_core_web_sm
```

### Basic Usage

#### Command Line Interface

```powershell
# Analyze an audio file
python cli.py analyze --input "audio/sample.wav" --output "results/"

# Batch process multiple files
python cli.py batch --input "audio/" --output "results/" --format json

# View system information
python cli.py info
```

#### Web Interface

```powershell
# Start the API server
python -m uvicorn api.server:app --host 127.0.0.1 --port 8000

# Open browser to http://127.0.0.1:8000
# Enjoy the 80s cosmic dashboard! 🌌
```

---

## 📚 Documentation

### Core Guides

- [**Installation Guide**](docs/INSTALLATION.md) - Detailed setup instructions
- [**User Guide**](docs/USER_GUIDE.md) - Complete usage documentation
- [**API Reference**](docs/API_REFERENCE.md) - REST API endpoints
- [**CLI Reference**](docs/CLI_REFERENCE.md) - Command-line interface
- [**Architecture Overview**](docs/ARCHITECTURE.md) - System design and components

### Development

- [**Development Guide**](docs/DEVELOPMENT.md) - Contributing and extending
- [**Security Guide**](docs/SECURITY.md) - Security features and best practices
- [**Testing Guide**](docs/TESTING.md) - Test suite and validation
- [**Deployment Guide**](docs/DEPLOYMENT.md) - Production deployment

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Lackadaisical Codex Extractor           │
├─────────────────────────────────────────────────────────────┤
│  🌌 Web Interface (80s Cosmic Theme)                       │
│  ├─ Live API monitoring    ├─ File upload                  │
│  ├─ Real-time progress     ├─ Results visualization        │
├─────────────────────────────────────────────────────────────┤
│  🚀 REST API (FastAPI)                                     │
│  ├─ /api/analyze          ├─ /api/health                   │
│  ├─ /api/auth             ├─ /api/results                  │
├─────────────────────────────────────────────────────────────┤
│  🎵 Audio Processing Pipeline                              │
│  ├─ loader.py (FFmpeg)    ├─ asr.py (Whisper)             │
│  ├─ acoustic.py (YIN)     ├─ nlp.py (spaCy)               │
├─────────────────────────────────────────────────────────────┤
│  🔐 Security Layer                                         │
│  ├─ JWT Authentication    ├─ AES-GCM Encryption           │
│  ├─ Rate Limiting         ├─ Audit Logging                │
├─────────────────────────────────────────────────────────────┤
│  💾 Data Layer                                             │
│  ├─ SQLCipher Database    ├─ Encrypted File Storage       │
│  ├─ Schema Validation     ├─ Quality Metrics              │
└─────────────────────────────────────────────────────────────┘
```

---

## 🛡️ Security Features

### Enterprise-Grade Protection

- **🔐 JWT Authentication**: Secure token-based authentication
- **🔒 AES-GCM Encryption**: Military-grade file encryption
- **🏦 SQLCipher Database**: Encrypted data storage
- **🛡️ Password Hashing**: bcrypt with salt rounds
- **⚡ Rate Limiting**: Request throttling and abuse prevention
- **📝 Audit Logging**: Comprehensive security event tracking
- **🔍 Input Validation**: Robust file type and content validation

### Security Best Practices

- Secure file cleanup with cryptographic erasure
- Memory-safe processing with automatic cleanup
- No plain-text storage of sensitive data
- Comprehensive error handling without information leakage
- Production-ready session management

---

## 📊 Performance

### Typical Processing Times

| Audio Duration | Processing Time | Memory Usage |
|---------------|-----------------|--------------|
| 30 seconds    | ~10 seconds     | 500MB        |
| 2 minutes     | ~30 seconds     | 800MB        |
| 10 minutes    | ~2 minutes      | 1.2GB        |

### Supported Formats

**Audio Input**: WAV, MP3, FLAC, OGG, M4A, AAC, WMA  
**Export Formats**: JSON (schema-validated), Raw JSON, Summary

---

## 🎨 Web Interface

### 80s Retro Cosmic Theme

Experience audio analysis like never before with our stunning **80s synthwave aesthetic**:

- **🌌 Deep Space Ambiance**: Dark cosmic background with neon accents
- **⚡ Animated Glitch Effects**: Dynamic visual feedback and transitions
- **🎵 Real-Time Monitoring**: Live API status with zero placeholder data
- **💫 Neon Glow Elements**: Blue/green/teal/purple color palette
- **🤖 Old School Typography**: Leet era fonts with modern responsiveness
- **📊 Live System Stats**: CPU, memory, and component status display

### Features

- Drag & drop file upload with validation
- Real-time analysis progress tracking
- Beautiful results visualization
- Live API connection monitoring
- Responsive design for all screen sizes

---

## 🧪 Testing

### Test Coverage

- **Unit Tests**: Core module functionality
- **Integration Tests**: API endpoint validation
- **Performance Tests**: Memory and speed benchmarks
- **Security Tests**: Authentication and encryption validation

```powershell
# Run test suite
pytest tests/ -v

# Performance benchmarks
pytest tests/performance/ --benchmark-only

# Security validation
pytest tests/security/ -v
```

---

## 📦 Deployment

### Standalone Executable

Create a single-file Windows executable:

```powershell
# Build standalone EXE
python build.py --target windows

# Result: dist/LackadaisicalCodexExtractor.exe
```

### Production Server

```powershell
# Production API server
uvicorn api.server:app --host 0.0.0.0 --port 8000 --workers 4

# With HTTPS (recommended)
uvicorn api.server:app --ssl-keyfile key.pem --ssl-certfile cert.pem
```

---

## 🤝 Contributing

We welcome contributions! Please see our [Development Guide](docs/DEVELOPMENT.md) for details.

### Development Setup

```powershell
# Install development dependencies
pip install -r requirements-dev.txt

# Run tests
pytest

# Code formatting
black core/ api/ tests/
```

---

## 📄 License

This project is licensed under the MIT License - see [LICENSE.md](LICENSE.md) for details.

---

## 🆘 Support

- **Documentation**: [docs/](docs/)
- **Issues**: [GitHub Issues](https://github.com/lackadaisical-security/codex-extractor/issues)
- **Security**: [security@lackadaisical-security.com](mailto:security@lackadaisical-security.com)
- **Website**: [https://lackadaisical-security.com](https://lackadaisical-security.com)

---

## 🎉 Acknowledgments

- **Whisper ASR**: OpenAI's speech recognition model
- **spaCy**: Industrial-strength NLP library
- **librosa**: Audio analysis in Python
- **FastAPI**: Modern, fast web framework
- **Praat/Parselmouth**: Phonetic analysis toolkit

---

*Built with 💜 by Lackadaisical Security*

**© 2025 Lackadaisical Security. All rights reserved.**
