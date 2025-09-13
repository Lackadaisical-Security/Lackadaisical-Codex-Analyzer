# API Reference

Complete REST API documentation for the Lackadaisical Codex Extractor.

## Base URL

```
http://127.0.0.1:8000
```

For production deployments, use HTTPS:
```
https://your-domain.com
```

## Authentication

The API uses JWT (JSON Web Token) authentication for secure access.

### Authentication Flow

1. **Register/Login** to get JWT token
2. **Include token** in Authorization header for protected endpoints
3. **Refresh token** when expired

### Headers

```http
Authorization: Bearer <jwt_token>
Content-Type: application/json
```

## Endpoints Overview

| Endpoint | Method | Auth Required | Description |
|----------|--------|---------------|-------------|
| `/` | GET | ❌ | Web dashboard |
| `/api/health` | GET | ❌ | API health check |
| `/api/auth/register` | POST | ❌ | User registration |
| `/api/auth/login` | POST | ❌ | User login |
| `/api/analyze` | POST | ✅ | Analyze audio file |
| `/api/status/{task_id}` | GET | ✅ | Check analysis status |
| `/api/results/{task_id}` | GET | ✅ | Get analysis results |
| `/v1/system/info` | GET | ❌ | System information |
| `/v1/docs` | GET | ❌ | Interactive API docs |

## Authentication Endpoints

### Register User

Register a new user account.

```http
POST /api/auth/register
```

**Request Body:**
```json
{
  "username": "string",
  "password": "string",
  "email": "string" (optional)
}
```

**Response:**
```json
{
  "access_token": "jwt_token_here",
  "token_type": "bearer",
  "user_id": "user_uuid"
}
```

**Example:**
```bash
curl -X POST "http://127.0.0.1:8000/api/auth/register" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "testuser",
    "password": "securepassword123"
  }'
```

### Login User

Authenticate existing user.

```http
POST /api/auth/login
```

**Request Body:**
```json
{
  "username": "string",
  "password": "string"
}
```

**Response:**
```json
{
  "access_token": "jwt_token_here",
  "token_type": "bearer",
  "expires_in": 3600
}
```

## Analysis Endpoints

### Analyze Audio

Upload and analyze an audio file.

```http
POST /api/analyze
```

**Headers:**
```http
Authorization: Bearer <token>
Content-Type: multipart/form-data
```

**Form Data:**
- `file`: Audio file (WAV, MP3, FLAC, OGG, M4A, AAC, WMA)

**Query Parameters:**
- `max_duration` (optional): Maximum duration to process (seconds)
- `skip_translation` (optional): Skip translation analysis (boolean)
- `skip_alignment` (optional): Skip feature alignment (boolean)
- `validate_schema` (optional): Validate output schema (boolean, default: true)
- `priority` (optional): Job priority (normal, high, low)

**Response:**
```json
{
  "task_id": "uuid",
  "status": "processing",
  "message": "Analysis started"
}
```

**Example:**
```bash
curl -X POST "http://127.0.0.1:8000/api/analyze" \
  -H "Authorization: Bearer <token>" \
  -F "file=@audio_sample.wav" \
  -F "max_duration=60"
```

### Check Analysis Status

Check the status of an analysis job.

```http
GET /api/status/{task_id}
```

**Parameters:**
- `task_id`: UUID of the analysis task

**Response:**
```json
{
  "task_id": "uuid",
  "status": "processing|completed|failed",
  "progress": 75,
  "message": "Processing audio features...",
  "error": null
}
```

**Status Values:**
- `queued`: Task is waiting to be processed
- `processing`: Task is currently being processed
- `completed`: Task completed successfully
- `failed`: Task failed with error

### Get Analysis Results

Retrieve completed analysis results.

```http
GET /api/results/{task_id}
```

**Parameters:**
- `task_id`: UUID of the completed analysis task

**Response:**
```json
{
  "task_id": "uuid",
  "status": "completed",
  "results": {
    "audio_analysis": { ... },
    "speech_recognition": { ... },
    "linguistic_analysis": { ... },
    "feature_alignment": { ... },
    "quality_metrics": { ... }
  },
  "metadata": {
    "processing_time": 15.2,
    "file_size": 2048576,
    "audio_duration": 30.5
  }
}
```

## System Endpoints

### Health Check

Check API health and system status.

```http
GET /api/health
```

**Response:**
```json
{
  "status": "healthy",
  "timestamp": "2025-09-05T10:30:00Z",
  "version": "1.0.0",
  "api_version": "v1",
  "cpu_usage": 25,
  "memory_usage": 45,
  "active_modules": [
    "whisper_asr",
    "spacy_nlp",
    "librosa_audio",
    "feature_alignment",
    "json_export"
  ],
  "components": {
    "audio_processor": "Available",
    "speech_recognition": "Available",
    "nlp_engine": "Available",
    "feature_alignment": "Available",
    "export_system": "Available"
  }
}
```

### System Information

Get detailed system information.

```http
GET /v1/system/info
```

**Response:**
```json
{
  "application": {
    "name": "Lackadaisical Codex Extractor",
    "version": "1.0.0",
    "description": "Production-grade audio analysis system"
  },
  "system": {
    "platform": "Windows",
    "python_version": "3.11.5",
    "architecture": "x64"
  },
  "components": {
    "whisper": "Available",
    "spacy": "Available",
    "librosa": "Available"
  },
  "supported_formats": [
    ".wav", ".mp3", ".flac", ".ogg", ".m4a", ".aac", ".wma"
  ],
  "models": [
    "en_core_web_sm",
    "whisper-base"
  ]
}
```

## Error Responses

All endpoints return consistent error responses:

```json
{
  "error": "Error type",
  "detail": "Detailed error message",
  "timestamp": "2025-09-05T10:30:00Z",
  "path": "/api/analyze"
}
```

### Common HTTP Status Codes

| Code | Meaning | Description |
|------|---------|-------------|
| 200 | OK | Request successful |
| 201 | Created | Resource created successfully |
| 400 | Bad Request | Invalid request data |
| 401 | Unauthorized | Authentication required |
| 403 | Forbidden | Insufficient permissions |
| 404 | Not Found | Resource not found |
| 422 | Validation Error | Request validation failed |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Server error |

## Rate Limiting

The API implements rate limiting to prevent abuse:

- **Authentication endpoints**: 5 requests per minute per IP
- **Analysis endpoints**: 10 requests per minute per user
- **System endpoints**: 60 requests per minute per IP

Rate limit headers are included in responses:

```http
X-RateLimit-Limit: 10
X-RateLimit-Remaining: 7
X-RateLimit-Reset: 1630000000
```

## Example Workflows

### Complete Analysis Workflow

1. **Register/Login:**
   ```bash
   curl -X POST "http://127.0.0.1:8000/api/auth/login" \
     -H "Content-Type: application/json" \
     -d '{"username": "user", "password": "pass"}'
   ```

2. **Start Analysis:**
   ```bash
   curl -X POST "http://127.0.0.1:8000/api/analyze" \
     -H "Authorization: Bearer <token>" \
     -F "file=@audio.wav"
   ```

3. **Check Status:**
   ```bash
   curl "http://127.0.0.1:8000/api/status/task-uuid" \
     -H "Authorization: Bearer <token>"
   ```

4. **Get Results:**
   ```bash
   curl "http://127.0.0.1:8000/api/results/task-uuid" \
     -H "Authorization: Bearer <token>"
   ```

### Python SDK Example

```python
import requests
import time

class CodexExtractorClient:
    def __init__(self, base_url="http://127.0.0.1:8000"):
        self.base_url = base_url
        self.token = None
    
    def login(self, username, password):
        response = requests.post(
            f"{self.base_url}/api/auth/login",
            json={"username": username, "password": password}
        )
        self.token = response.json()["access_token"]
    
    def analyze_file(self, file_path):
        with open(file_path, "rb") as f:
            response = requests.post(
                f"{self.base_url}/api/analyze",
                headers={"Authorization": f"Bearer {self.token}"},
                files={"file": f}
            )
        return response.json()["task_id"]
    
    def wait_for_results(self, task_id):
        while True:
            response = requests.get(
                f"{self.base_url}/api/status/{task_id}",
                headers={"Authorization": f"Bearer {self.token}"}
            )
            status = response.json()
            
            if status["status"] == "completed":
                break
            elif status["status"] == "failed":
                raise Exception(status.get("error", "Analysis failed"))
            
            time.sleep(2)
        
        # Get results
        response = requests.get(
            f"{self.base_url}/api/results/{task_id}",
            headers={"Authorization": f"Bearer {self.token}"}
        )
        return response.json()

# Usage
client = CodexExtractorClient()
client.login("username", "password")
task_id = client.analyze_file("audio.wav")
results = client.wait_for_results(task_id)
print(results)
```

## Interactive Documentation

For interactive API exploration, visit:
```
http://127.0.0.1:8000/v1/docs
```

This provides a Swagger UI interface for testing all endpoints directly from your browser.

## WebSocket Support (Coming Soon)

Future versions will include WebSocket support for real-time progress updates:

```javascript
const ws = new WebSocket('ws://127.0.0.1:8000/ws/analysis/task-id');
ws.onmessage = (event) => {
    const progress = JSON.parse(event.data);
    console.log(`Progress: ${progress.percent}%`);
};
```
