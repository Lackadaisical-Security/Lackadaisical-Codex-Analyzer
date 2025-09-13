# Installation Guide

Complete setup instructions for the Lackadaisical Codex Extractor.

## System Requirements

### Minimum Requirements

- **Operating System**: Windows 10/11 (64-bit)
- **Python**: 3.11+ (64-bit)
- **RAM**: 4GB minimum, 8GB recommended
- **Storage**: 2GB free space
- **Audio**: Standard audio drivers

### Recommended Requirements

- **RAM**: 16GB for large audio files
- **CPU**: Multi-core processor (4+ cores)
- **Storage**: SSD for faster processing
- **Network**: Internet connection for initial model downloads

## Step-by-Step Installation

### 1. Python Installation

1. Download Python 3.11+ from [python.org](https://python.org)
2. **Important**: Check "Add Python to PATH" during installation
3. Verify installation:
   ```powershell
   python --version
   # Should show Python 3.11.x or higher
   ```

### 2. Project Setup

1. Extract the Lackadaisical Codex Extractor to your desired location:
   ```
   C:\Projects\Lackadaisical-Codex-Extractor\
   ```

2. Open PowerShell as Administrator and navigate to the project:
   ```powershell
   cd "C:\Projects\Lackadaisical-Codex-Extractor"
   ```

### 3. Virtual Environment

Create and activate a virtual environment:

```powershell
# Create virtual environment
python -m venv .venv

# Activate virtual environment
.venv\Scripts\Activate.ps1

# If you get execution policy error, run this first:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### 4. Install Dependencies

```powershell
# Install all required packages
pip install -r requirements.txt

# Download spaCy language model
python -m spacy download en_core_web_sm
```

### 5. Verify Installation

```powershell
# Test CLI
python cli.py info

# Test security module
python core/security.py

# Start API server (optional)
python -m uvicorn api.server:app --host 127.0.0.1 --port 8000
```

## Common Issues and Solutions

### PowerShell Execution Policy

If you get execution policy errors:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### Missing Visual C++ Redistributables

Some packages require Visual C++ redistributables:

1. Download from [Microsoft](https://docs.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist)
2. Install the x64 version
3. Restart PowerShell and retry installation

### FFmpeg Issues

FFmpeg is included in the project, but if you encounter issues:

1. Download FFmpeg from [ffmpeg.org](https://ffmpeg.org)
2. Extract to `ffmpeg/` directory in project root
3. Ensure `ffmpeg.exe` is in your PATH

### Memory Issues

For large audio files:

1. Increase virtual memory (pagefile)
2. Close other applications
3. Process files in smaller chunks using batch mode

## Security Setup

### Initial Security Configuration

```powershell
# Initialize secure database
python core/security.py --init-db

# Generate self-signed certificates (for HTTPS)
python core/security.py --init-cert
```

### Authentication Setup

1. Create your first admin user:
   ```powershell
   python cli.py create-user --username admin --role admin
   ```

2. Set environment variables for production:
   ```powershell
   $env:SECRET_KEY = "your-secret-key-here"
   $env:DATABASE_URL = "sqlite+pysqlcipher://:password@/database.db"
   ```

## Development Setup

### Additional Development Dependencies

```powershell
pip install -r requirements-dev.txt
```

### Pre-commit Hooks

```powershell
pre-commit install
```

### Testing Environment

```powershell
# Run full test suite
pytest tests/ -v

# Run with coverage
pytest --cov=core tests/
```

## Troubleshooting

### Performance Issues

1. **Slow processing**: Ensure sufficient RAM and CPU resources
2. **Memory errors**: Process smaller audio files or increase virtual memory
3. **Disk space**: Ensure sufficient free space for temporary files

### Network Issues

1. **Model download failures**: Check internet connection and firewall
2. **API connection issues**: Verify port availability (default: 8000)
3. **HTTPS certificate errors**: Use self-signed certificates for development

### Audio Format Issues

1. **Unsupported formats**: Convert to WAV, MP3, or FLAC
2. **Corrupted files**: Verify audio file integrity
3. **Large files**: Use FFmpeg to reduce bitrate/duration

## Next Steps

After successful installation:

1. Read the [User Guide](USER_GUIDE.md)
2. Try the [API Reference](API_REFERENCE.md)
3. Explore the [CLI Reference](CLI_REFERENCE.md)
4. Review [Security Best Practices](SECURITY.md)

## Support

If you encounter issues:

1. Check this troubleshooting guide
2. Review the [FAQ](FAQ.md)
3. Search existing [GitHub Issues](https://github.com/lackadaisical-security/codex-extractor/issues)
4. Contact support: [support@lackadaisical-security.com](mailto:support@lackadaisical-security.com)
