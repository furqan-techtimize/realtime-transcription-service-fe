# Real-Time Transcription Frontend

A modern web interface for real-time speech-to-text transcription with AWS Transcribe and Deepgram support.

🌐 **[Live Demo](https://yourusername.github.io/realtime-transcription-frontend/)**

## ✨ Features

- 🎤 **Live Recording** - Real-time microphone transcription
- 📁 **File Upload** - Transcribe pre-recorded audio files
- ⚡ **Speed Control** - Process files at 0.5x to 4x speed
- 👥 **Speaker Diarization** - Identify different speakers
- 🔬 **Provider Comparison** - Compare AWS vs Deepgram side-by-side
- 📊 **Live Metrics** - Confidence, latency, WPM, accuracy
- 💾 **Export Options** - Download as TXT or JSON
- 🎨 **Modern UI** - Clean, responsive design

## 🚀 Quick Start

### Option 1: Use with Hosted Backend

Simply open `index.html` in your browser and connect to a running backend:

```javascript
// The WebSocket URL is configurable in the HTML
const WS_URL = 'ws://localhost:8765';  // Local development
// or
const WS_URL = 'wss://your-backend.onrender.com';  // Production
```

### Option 2: GitHub Pages (Recommended)

Deploy for free on GitHub Pages:

1. Fork this repository
2. Go to **Settings** → **Pages**
3. Source: Deploy from **main** branch
4. Your site will be live at: `https://yourusername.github.io/realtime-transcription-frontend/`

### Option 3: Local Development

```bash
# Clone the repository
git clone https://github.com/yourusername/realtime-transcription-frontend.git
cd realtime-transcription-frontend

# Open in browser (or use a local server)
# On Windows
start index.html

# Or use Python's built-in server
python -m http.server 8080
# Visit http://localhost:8080
```

## 🔧 Configuration

### Connect to Your Backend

Edit the WebSocket URL in `index.html`:

```javascript
// Line ~700 - Update this to your backend URL
const WS_URL = window.location.hostname === 'localhost' 
    ? 'ws://localhost:8765'
    : 'wss://your-backend-url.com';
```

### Customize Settings

```html
<!-- Default provider -->
<button class="provider-btn active" data-provider="deepgram">Deepgram</button>

<!-- Available speeds -->
<input type="range" min="0.5" max="4" step="0.5" value="1" id="playbackSpeedSlider">

<!-- Enable/disable features -->
<input type="checkbox" id="diarizationToggle" checked>
```

## 📖 Usage

### Live Recording

1. Click **"Start Recording"**
2. Allow microphone access
3. Speak clearly into your microphone
4. Real-time transcription appears as you speak
5. Click **"Stop"** when finished
6. Download transcript as TXT or JSON

### File Upload

1. Click **"📁 Upload Audio File"** or drag & drop
2. Supported formats: MP3, WAV, M4A, FLAC, OGG
3. Select provider: **AWS Transcribe** or **Deepgram**
4. Choose model and enable diarization if needed
5. Adjust playback speed (1x-4x for faster processing)
6. Click **"Transcribe"**
7. Download results when complete

### Provider Comparison

1. Upload an audio file
2. Click **"🔬 Compare AWS vs Deepgram"**
3. Both providers transcribe the same audio
4. Download detailed comparison report:
   - Processing time comparison
   - Accuracy metrics
   - Speaker diarization analysis
   - Text similarity score
   - Side-by-side transcripts

## 🎨 Features Overview

### Supported Providers

**AWS Transcribe:**
- ✅ Standard, Medical, Call Center models
- ✅ Speaker diarization
- ⚠️ Auto-restarts every 5 minutes for long files
- 🎯 Best for: Medical/call center content

**Deepgram:**
- ✅ Nova-3, Nova-2, Enhanced, Base models
- ✅ Speaker diarization
- ✅ Supports files up to 1+ hour
- ⚡ Processes at up to 4x speed
- 🎯 Best for: General transcription, long files

### Audio Visualizer

Real-time audio visualization shows:
- 🎵 Live waveform during recording
- 📊 50-bar frequency spectrum
- 🔊 Audio level indicators

### Metrics Dashboard

Track transcription quality:
- ⏱️ **Duration** - Total transcription time
- 📝 **Word Count** - Total words transcribed
- ⚡ **WPM** - Words per minute
- ✅ **Confidence** - Average confidence score
- 🚀 **Latency** - Processing delay
- 🎯 **Accuracy** - Estimated accuracy

## 🌐 Deployment Options

### GitHub Pages (Free, Easiest)

```bash
# Already set up! Just enable in Settings → Pages
# Your site: https://yourusername.github.io/realtime-transcription-frontend/
```

### Netlify (Free)

1. Sign up at [netlify.com](https://netlify.com)
2. Connect your GitHub repository
3. Deploy automatically on every push
4. Custom domain support

### Vercel (Free)

1. Sign up at [vercel.com](https://vercel.com)
2. Import from GitHub
3. Auto-deploy with every commit
4. Excellent performance

### Cloudflare Pages (Free)

1. Sign up at [pages.cloudflare.com](https://pages.cloudflare.com)
2. Connect repository
3. Unlimited bandwidth
4. Global CDN

## 📁 Project Structure

```
realtime-transcription-frontend/
├── index.html          # Main application (self-contained)
├── README.md           # This file
├── LICENSE             # MIT License
└── .gitignore         # Git ignore rules
```

## 🔌 Backend Requirements

This frontend requires a WebSocket backend server. Options:

1. **[realtime-transcription-service](https://github.com/yourusername/realtime-transcription-service)** - Python backend
2. Your own custom backend implementing the WebSocket protocol

### WebSocket Protocol

**Messages the frontend expects:**

```javascript
// Connection established
{ type: 'connection_established', connection_id: '...' }

// Transcription result
{ 
  type: 'transcription_result',
  data: {
    text: 'Hello world',
    confidence: 0.95,
    is_final: true,
    speaker: 0,
    timestamp: '2025-11-25T12:00:00'
  }
}

// Metrics update
{
  type: 'metrics_update',
  data: { duration, word_count, wpm, avg_confidence, avg_latency }
}

// Status messages
{ type: 'transcription_timeout', message: '...' }
{ type: 'transcription_reconnected', message: '...' }
{ type: 'queue_warning', message: '...' }
{ type: 'error', message: '...' }
```

## 🎯 Browser Support

- ✅ Chrome 80+
- ✅ Firefox 75+
- ✅ Safari 13+
- ✅ Edge 80+
- ⚠️ Requires WebSocket support
- ⚠️ Requires Web Audio API (for recording)

## 🐛 Troubleshooting

### Microphone Not Working

- Check browser permissions (click 🔒 in address bar)
- Only works on HTTPS (or localhost)
- Try refreshing the page

### File Upload Fails

- Check file format (MP3, WAV, M4A, FLAC, OGG)
- Maximum recommended size: 100MB
- For large files, use Deepgram provider

### WebSocket Connection Failed

- Verify backend is running
- Check WebSocket URL in code
- Look for CORS errors in console
- Ensure backend allows WebSocket connections

### AWS Memory Errors (Historical)

- ✅ Fixed with auto-restart every 5 minutes
- If issues persist, use Deepgram instead

## 🤝 Contributing

Contributions welcome! This is a static HTML file, so:

1. Fork the repository
2. Edit `index.html`
3. Test locally
4. Submit a Pull Request

## 📄 License

MIT License - see [LICENSE](LICENSE) file

## 🔗 Related Projects

- [realtime-transcription-service](https://github.com/yourusername/realtime-transcription-service) - Python backend
- [AWS Transcribe](https://aws.amazon.com/transcribe/)
- [Deepgram](https://deepgram.com/)

## 🆘 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/realtime-transcription-frontend/issues)
- **Backend Setup**: See backend repository README
- **API Keys**: Required on backend only (not in frontend)

## 🙏 Acknowledgments

Built with:
- Native JavaScript (no frameworks!)
- Web Audio API
- WebSocket API
- HTML5 & CSS3

---

**Note**: This is a static frontend that requires a backend WebSocket server. See the [backend repository](https://github.com/yourusername/realtime-transcription-service) for the server component.

Built with ❤️ for real-time transcription
