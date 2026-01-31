# 🎥 Language Transcription Backend

Backend server for the Multi-User Live Video/Audio Translation System with real-time speech translation, user authentication, and room management.

## 🚀 Features

- **🎤 Real-time Speech Translation**: Live audio processing with instant translation
- **👥 Multi-User Room Management**: Secure rooms with password protection
- **🔐 User Authentication**: Name-based user identification
- **🌐 Multi-Language Support**: Tamil, Hindi, Spanish, French, and 10+ languages
- **🔊 WebSocket Communication**: Real-time audio broadcasting
- **🛡️ Security**: Password validation and access control
- **🤖 AI/ML Pipeline**: STT → Translation → TTS

## 🛠️ Technology Stack

- **Node.js** with Express.js
- **WebSocket** for real-time communication
- **Python** for AI processing (STT, Translation, TTS)
- **Multer** for file uploads
- **Speech Recognition** (Google Speech API + offline fallback)
- **Language Translation** (Custom translation engine)
- **Text-to-Speech** (pyttsx3 for cross-platform TTS)

## 📋 Prerequisites

- **Node.js** (v14 or higher)
- **Python** (v3.10 or higher)
- **npm** or **yarn**

## 🚀 Installation

### 1. Clone the repository
```bash
git clone https://github.com/Suganthi528/language-transcription-backend.git
cd language-transcription-backend
```

### 2. Install Node.js Dependencies
```bash
npm install
```

### 3. Install Python Dependencies
```bash
python -m pip install -r requirements.txt
```

## 🏃‍♂️ Running the Server

```bash
npm start
```

Server will run on `http://localhost:5000`

## 🔄 API Endpoints

### Room Management
- `POST /create-room` - Create a new room with optional password
- `GET /rooms` - List all active rooms
- `WebSocket /` - Real-time communication

### Translation Pipeline
- `POST /translate-speech` - Complete speech translation pipeline
- `POST /live-translate` - Live video/audio translation
- `POST /stt` - Speech-to-text only
- `POST /translate` - Text translation only
- `POST /tts` - Text-to-speech only
- `GET /audio` - Get generated audio file

## 🌐 Supported Languages

- **Tamil (தமிழ்)** - Primary focus
- **Hindi (हिन्दी)**
- **Telugu (తెలుగు)**
- **Kannada (ಕನ್ನಡ)**
- **Malayalam (മലയാളം)**
- **Spanish, French, German, Italian**
- **Portuguese, Russian, Japanese, Korean, Chinese**

## 🔐 WebSocket Events

### Client to Server
```javascript
// Join a room
{
  type: 'join-room',
  roomId: 'room123',
  userId: 'user456',
  userName: 'Alice',
  password: 'secret123',
  language: 'ta'
}

// Send audio chunk
{
  type: 'audio-chunk',
  audioData: 'base64_audio_data',
  targetLang: 'ta',
  roomId: 'room123'
}

// Leave room
{
  type: 'leave-room'
}
```

### Server to Client
```javascript
// Room joined successfully
{
  type: 'room-joined',
  roomId: 'room123',
  userId: 'user456',
  userName: 'Alice',
  connectedUsers: [...]
}

// Translation result
{
  type: 'translated-audio',
  audioUrl: '/static/audio_123.wav',
  originalText: 'Hello',
  translatedText: 'வணக்கம்',
  fromUserName: 'Alice'
}

// Error handling
{
  type: 'join-error',
  message: 'Invalid room password'
}
```

## 📁 Project Structure

```
language-transcription-backend/
├── python/
│   ├── synthesize.py              # Text-to-Speech with multi-language support
│   ├── transcribe.py              # Speech-to-Text with Google API + offline fallback
│   ├── transcribe_offline.py     # Offline transcription fallback
│   └── translate.py               # Language translation engine
├── server.js                      # Main Express server with WebSocket support
├── package.json                   # Node.js dependencies
├── requirements.txt               # Python dependencies
├── README.md                      # This file
└── test files/                    # Test suite
    ├── debug_audio.py
    ├── final_test.py
    ├── system_status.py
    ├── test_live_endpoint.py
    ├── test_multiuser.py
    ├── test_name_password.py
    ├── test_pipeline.py
    └── test_system.py
```

## 🧪 Testing

### Run All Tests
```bash
python final_test.py
```

### Test Individual Components
```bash
# Test translation
python python/translate.py "Hello world" ta

# Test TTS
python python/synthesize.py "வணக்கம்" ta test.wav

# Test room system
python test_name_password.py

# Test multi-user functionality
python test_multiuser.py
```

## 🔧 Configuration

### Environment Variables
```bash
# Optional: Set custom port
PORT=5000

# Optional: Set Python path
PYTHON_PATH=/usr/bin/python3
```

### Dependencies

#### Node.js Dependencies
- express: Web framework
- ws: WebSocket library
- cors: Cross-origin resource sharing
- multer: File upload handling

#### Python Dependencies
- googletrans: Translation service
- pyttsx3: Text-to-speech
- SpeechRecognition: Speech-to-text
- numpy: Numerical computing
- requests: HTTP library
- pydub: Audio processing

## 🚨 Troubleshooting

### Common Issues

**"Module not found" errors**
```bash
npm install
python -m pip install -r requirements.txt
```

**"Port already in use"**
```bash
# Kill process on port 5000
npx kill-port 5000
```

**"Python command not found"**
```bash
# Use python3 instead of python
python3 -m pip install -r requirements.txt
```

**Translation not working**
- Check internet connection for Google Translate API
- Verify Python dependencies are installed
- Try offline fallback mode

## 🔄 API Usage Examples

### Create a Room
```javascript
fetch('http://localhost:5000/create-room', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    roomName: 'MeetingRoom',
    password: 'secret123',
    creatorName: 'Alice'
  })
})
```

### Translate Text
```javascript
fetch('http://localhost:5000/translate', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    text: 'Hello world',
    targetLang: 'ta'
  })
})
```

### Upload Audio for Translation
```javascript
const formData = new FormData();
formData.append('audio', audioBlob);
formData.append('targetLang', 'ta');

fetch('http://localhost:5000/live-translate', {
  method: 'POST',
  body: formData
})
```

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License.

## 👥 Authors

- **Suganthi528** - *Initial work* - [Suganthi528](https://github.com/Suganthi528)

## 🙏 Acknowledgments

- Google Speech Recognition API
- Node.js and Express.js communities
- Python TTS libraries
- WebSocket technology

---

**🎊 Ready to power real-time translation applications! 🌍**