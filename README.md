# Resumable File Uploads with Python-Flask

A modern web application that demonstrates resumable file uploads using Flask and Resumable.js. This project allows users to upload large files reliably by splitting them into smaller chunks, with the ability to pause, resume, and recover from network interruptions.

## Features

- **Chunked File Uploads**: Files are split into manageable chunks (8MB by default) for more reliable transfers
- **Resumable Uploads**: Interrupted uploads can be resumed from where they left off
- **Pause/Resume Functionality**: Users can pause and resume uploads at any time
- **Drag & Drop Interface**: Modern, user-friendly interface for file selection
- **Progress Tracking**: Real-time visual feedback on upload progress
- **Automatic Cleanup**: Temporary chunks are automatically removed after a configurable time period
- **File Integrity Verification**: Optional verification to ensure uploaded files are complete and uncorrupted

## How It Works

1. The client-side (using Resumable.js) splits files into chunks
2. Each chunk is uploaded individually to the server
3. The server stores chunks temporarily
4. Once all chunks are received, the server assembles them into the complete file
5. If an upload is interrupted, only the missing chunks need to be re-uploaded

## Project Structure

```
├── run.py                  # Application entry point
├── src/
│   ├── __init__.py
│   ├── app.py              # Flask application and server-side logic
│   ├── static/
│   │   ├── css/
│   │   │   └── styles.css  # Application styling
│   │   └── js/
│   │       ├── main.js     # Custom JavaScript for the application
│   │       └── resumable.js # Resumable.js library
│   └── templates/
│       └── index.html      # Main application page
└── uploads/                # Created at runtime to store uploaded files
    └── temp/               # Temporary storage for file chunks
```

## Configuration

The application can be configured by modifying the following settings in `app.py`:

- `UPLOAD_ROOT`: Directory where uploaded files are stored
- `CHUNK_TTL_HOURS`: Time-to-live for temporary chunks (default: 6 hours)
- `VERIFY_UPLOADS`: Enable/disable file integrity verification

## Getting Started

### Prerequisites

- Python 3.6 or higher
- Flask

### Installation

1. Clone the repository
2. Install dependencies:
   ```
   pip install flask
   ```

### Running the Application

1. Start the server:
   ```
   python run.py
   ```
2. Open a web browser and navigate to `http://localhost:5000`
3. Drag and drop files or use the "Select Files" button to begin uploading

## Technical Details

- **Chunk Size**: Default is 8MB, configurable in `main.js`
- **Simultaneous Uploads**: 4 chunks at a time by default
- **Retry Logic**: Failed chunks are retried up to 6 times with a 4-second interval

## Use Cases

- Uploading large files over unreliable networks
- Media file uploads (videos, high-resolution images)
- Document management systems
- Backup solutions