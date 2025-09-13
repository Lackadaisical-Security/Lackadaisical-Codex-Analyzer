# User Guide

Complete guide to using the Lackadaisical Codex Extractor for audio analysis.

## Table of Contents

- [Getting Started](#getting-started)
- [Command Line Interface](#command-line-interface)
- [Web Interface](#web-interface)
- [Analysis Features](#analysis-features)
- [Output Formats](#output-formats)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Getting Started

### Prerequisites

Ensure you have completed the [Installation Guide](INSTALLATION.md) before proceeding.

### First Analysis

Let's start with a simple audio analysis:

```powershell
# Analyze a single audio file
python cli.py analyze --input "samples/test.wav" --output "results/"
```

This will process the audio file and generate a comprehensive analysis in the `results/` directory.

## Command Line Interface

The CLI provides powerful batch processing and analysis capabilities.

### Basic Commands

#### Analyze Command

Analyze a single audio file:

```powershell
python cli.py analyze --input "audio.wav" --output "results/"
```

**Options:**
- `--input, -i`: Input audio file path
- `--output, -o`: Output directory for results
- `--format`: Output format (json, summary, raw)
- `--max-duration`: Maximum duration to process (seconds)
- `--skip-nlp`: Skip natural language processing
- `--skip-alignment`: Skip feature alignment
- `--verbose, -v`: Enable verbose logging

#### Batch Command

Process multiple files at once:

```powershell
python cli.py batch --input "audio_folder/" --output "results/" --format json
```

**Options:**
- `--input, -i`: Input directory containing audio files
- `--output, -o`: Output directory for results
- `--format`: Output format for all files
- `--workers`: Number of parallel workers (default: 2)
- `--filter`: File extension filter (e.g., "wav,mp3")

#### Info Command

Display system and component information:

```powershell
python cli.py info
```

This shows:
- System specifications
- Available components
- Supported audio formats
- Model information

#### Summary Command

Generate a summary report of processed files:

```powershell
python cli.py summary --input "results/" --output "report.html"
```

### Advanced Usage

#### Custom Configuration

Create a configuration file for repeated settings:

```json
{
  "audio": {
    "max_duration": 300,
    "sample_rate": 16000
  },
  "nlp": {
    "skip_sentiment": false,
    "include_embeddings": true
  },
  "output": {
    "format": "json",
    "validate_schema": true
  }
}
```

Use with:
```powershell
python cli.py analyze --config config.json --input audio.wav
```

#### Batch Processing with Filters

Process only specific file types:

```powershell
python cli.py batch --input "recordings/" --filter "wav,flac" --output "results/"
```

#### Progress Monitoring

Monitor progress with detailed output:

```powershell
python cli.py analyze --input large_file.wav --verbose --progress
```

## Web Interface

The cosmic-themed web interface provides an intuitive way to analyze audio files.

### Accessing the Interface

1. Start the API server:
   ```powershell
   python -m uvicorn api.server:app --host 127.0.0.1 --port 8000
   ```

2. Open your browser to: `http://127.0.0.1:8000`

### Interface Features

#### 🌌 Cosmic Dashboard

- **80s Retro Theme**: Synthwave aesthetics with neon colors
- **Live Status Monitoring**: Real-time API health display
- **Animated Effects**: Glitch animations and cosmic background

#### File Upload

1. **Drag & Drop**: Drag audio files directly onto the upload area
2. **File Browser**: Click "BROWSE FILES" to select audio files
3. **Format Validation**: Automatic validation of supported formats

#### Analysis Process

1. **Upload**: File is securely uploaded and validated
2. **Processing**: Real-time progress updates with cosmic animations
3. **Results**: Beautiful visualization of analysis results

#### Results Visualization

- **Audio Analysis**: Waveform, frequency analysis, pitch contours
- **Speech Recognition**: Transcription with confidence scores
- **Linguistic Analysis**: Sentiment, entities, semantic features
- **Quality Metrics**: Processing quality and reliability scores

### Authentication

For secure access (when authentication is enabled):

1. **Register**: Create a new account
2. **Login**: Authenticate with username/password
3. **Token Management**: Automatic token refresh

## Analysis Features

### Audio Processing

#### Supported Formats

- **WAV**: Uncompressed, high quality
- **MP3**: Compressed, widely compatible
- **FLAC**: Lossless compression
- **OGG**: Open-source alternative
- **M4A/AAC**: Apple/iTunes format
- **WMA**: Windows Media Audio

#### Audio Metrics

- **Duration**: Total length in seconds
- **Sample Rate**: Samples per second (Hz)
- **Bit Depth**: Bits per sample
- **Channels**: Mono/stereo configuration
- **File Size**: Total file size in bytes

### Speech Recognition

#### Whisper ASR Integration

- **High Accuracy**: State-of-the-art speech recognition
- **Multiple Languages**: Primarily English, with multi-language support
- **Confidence Scoring**: Per-word confidence levels
- **Timestamp Alignment**: Precise word-level timing

#### Recognition Output

```json
{
  "text": "Hello world, this is a test.",
  "segments": [
    {
      "id": 0,
      "seek": 0,
      "start": 0.0,
      "end": 2.5,
      "text": " Hello world, this is a test.",
      "tokens": [50364, 2425, 1002, 11, 341, 307, 257, 1500, 13, 50489],
      "temperature": 0.0,
      "avg_logprob": -0.15,
      "compression_ratio": 1.2,
      "no_speech_prob": 0.01
    }
  ]
}
```

### Acoustic Analysis

#### Pitch Extraction (YIN Algorithm)

- **Fundamental Frequency**: F0 detection
- **Pitch Contours**: Melodic patterns
- **Voicing Detection**: Voiced vs. unvoiced segments

#### Formant Analysis

- **F1, F2, F3**: First three formant frequencies
- **Bandwidth**: Formant bandwidths
- **Vowel Classification**: Automatic vowel identification

#### Spectral Features

- **MFCC**: Mel-frequency cepstral coefficients
- **Spectral Centroid**: Brightness measure
- **Spectral Rolloff**: High-frequency content
- **Zero Crossing Rate**: Frequency domain measure

### Natural Language Processing

#### spaCy Pipeline

- **Tokenization**: Word and sentence boundaries
- **Part-of-Speech**: Grammatical categories
- **Named Entities**: Person, location, organization detection
- **Dependency Parsing**: Grammatical relationships

#### Sentiment Analysis

- **VADER**: Rule-based sentiment analysis
- **TextBlob**: Statistical sentiment analysis
- **Emotion Detection**: Multi-class emotion recognition

#### Semantic Features

- **Sentence Embeddings**: Vector representations
- **Similarity Scores**: Semantic similarity measures
- **Topic Modeling**: Automatic topic detection

### Feature Alignment

#### Temporal Synchronization

- **Word-Level**: Align words with audio timestamps
- **Syllable-Level**: Syllable boundary detection
- **Phoneme-Level**: Individual sound alignment

#### Cadence Analysis

- **Speaking Rate**: Words per minute
- **Pause Detection**: Silent intervals
- **Rhythm Patterns**: Prosodic features

## Output Formats

### JSON Schema

The primary output format is schema-validated JSON:

```json
{
  "metadata": {
    "file_path": "audio.wav",
    "duration": 30.5,
    "processing_time": 15.2,
    "timestamp": "2025-09-05T10:30:00Z"
  },
  "audio_analysis": {
    "sample_rate": 16000,
    "duration": 30.5,
    "channels": 1,
    "pitch": {
      "f0_mean": 120.5,
      "f0_std": 15.2,
      "voiced_fraction": 0.75
    },
    "formants": {
      "f1_mean": 650.0,
      "f2_mean": 1200.0,
      "f3_mean": 2500.0
    },
    "spectral": {
      "mfcc": [...],
      "spectral_centroid": 1500.0,
      "spectral_rolloff": 3500.0
    }
  },
  "speech_recognition": {
    "text": "Hello world, this is a test.",
    "confidence": 0.95,
    "segments": [...],
    "word_timestamps": [...]
  },
  "linguistic_analysis": {
    "tokens": [...],
    "entities": [...],
    "sentiment": {
      "compound": 0.5,
      "positive": 0.7,
      "neutral": 0.2,
      "negative": 0.1
    },
    "embeddings": [...]
  },
  "quality_metrics": {
    "overall_score": 0.92,
    "audio_quality": 0.95,
    "recognition_confidence": 0.94,
    "processing_success": true
  }
}
```

### Summary Format

Human-readable summary for quick review:

```
=== AUDIO ANALYSIS SUMMARY ===
File: audio.wav
Duration: 30.5 seconds
Quality Score: 92%

Speech Recognition:
"Hello world, this is a test."
Confidence: 95%

Acoustic Features:
- Average Pitch: 120.5 Hz
- Speaking Rate: 150 WPM
- Voiced Speech: 75%

Sentiment Analysis:
- Overall: Positive (70%)
- Compound Score: 0.5

Processing Time: 15.2 seconds
```

### Raw Format

Unprocessed output for advanced users:

```json
{
  "raw_audio_features": {...},
  "raw_nlp_output": {...},
  "raw_asr_output": {...},
  "processing_logs": [...]
}
```

## Best Practices

### Audio Quality

#### Optimal Recording Conditions

- **Quiet Environment**: Minimize background noise
- **Good Microphone**: Use quality recording equipment
- **Consistent Levels**: Avoid clipping and distortion
- **Stable Position**: Keep microphone distance consistent

#### File Specifications

- **Sample Rate**: 16kHz minimum, 44.1kHz recommended
- **Bit Depth**: 16-bit minimum, 24-bit preferred
- **Format**: WAV or FLAC for best quality
- **Duration**: 5 seconds to 10 minutes optimal

### Processing Efficiency

#### Large Files

- **Segment Processing**: Break into smaller chunks
- **Batch Processing**: Use batch command for multiple files
- **Resource Monitoring**: Monitor RAM and CPU usage
- **Disk Space**: Ensure adequate free space

#### Performance Optimization

- **Close Applications**: Free up system resources
- **SSD Storage**: Use fast storage for temporary files
- **Adequate RAM**: 8GB+ recommended for large files
- **Multi-core CPU**: Better for parallel processing

### Security Considerations

#### Sensitive Data

- **File Encryption**: Enable AES-GCM encryption
- **Secure Deletion**: Use secure file cleanup
- **Access Control**: Implement user authentication
- **Audit Logging**: Enable comprehensive logging

#### Privacy Protection

- **Local Processing**: Keep data on local machine
- **Temporary Files**: Automatic cleanup after processing
- **No Cloud Upload**: All processing happens locally
- **Data Retention**: Control how long results are stored

## Troubleshooting

### Common Issues

#### Installation Problems

**Issue**: Python package installation fails
```
Solution: Ensure you have Visual C++ redistributables installed
```

**Issue**: spaCy model download fails
```
Solution: python -m spacy download en_core_web_sm --user
```

#### Processing Errors

**Issue**: "Unsupported audio format"
```
Solution: Convert to WAV, MP3, or FLAC format
```

**Issue**: "Out of memory" error
```
Solution: Process shorter segments or increase virtual memory
```

**Issue**: "FFmpeg not found"
```
Solution: Ensure FFmpeg is in PATH or use bundled version
```

#### Performance Issues

**Issue**: Slow processing
```
Solutions:
- Close other applications
- Use SSD storage
- Process smaller files
- Increase RAM
```

**Issue**: High CPU usage
```
Solutions:
- Reduce worker count in batch processing
- Process files sequentially
- Lower audio quality settings
```

### Error Messages

#### Audio Processing Errors

- **"Invalid audio file"**: File is corrupted or unsupported
- **"Audio too short"**: File must be at least 1 second
- **"Sample rate too low"**: Minimum 8kHz required

#### API Errors

- **401 Unauthorized**: Check authentication token
- **429 Rate Limited**: Reduce request frequency
- **413 File Too Large**: Reduce file size or increase limits

#### System Errors

- **"Insufficient disk space"**: Free up storage space
- **"Permission denied"**: Run with appropriate permissions
- **"Port already in use"**: Change API server port

### Getting Help

1. **Check Logs**: Review error messages in console output
2. **Documentation**: Consult this guide and API reference
3. **FAQ**: Check frequently asked questions
4. **Support**: Contact support@lackadaisical-security.com
5. **GitHub Issues**: Report bugs and feature requests

## Advanced Features

### Custom Configurations

Create project-specific settings:

```json
{
  "audio_settings": {
    "max_duration": 600,
    "normalize": true,
    "noise_reduction": true
  },
  "nlp_settings": {
    "include_pos_tags": true,
    "extract_entities": true,
    "sentiment_threshold": 0.1
  },
  "output_settings": {
    "include_raw_data": false,
    "compress_output": true,
    "validation_strict": true
  }
}
```

### Scripting and Automation

#### Python Integration

```python
from cli import CodexExtractor

extractor = CodexExtractor()
results = extractor.analyze_file("audio.wav")
print(f"Sentiment: {results['linguistic_analysis']['sentiment']['compound']}")
```

#### Batch Scripts

```powershell
# Process all WAV files in a directory
Get-ChildItem "*.wav" | ForEach-Object {
    python cli.py analyze --input $_.Name --output "results/"
}
```

This completes the comprehensive User Guide. Users now have detailed instructions for every aspect of the system!
