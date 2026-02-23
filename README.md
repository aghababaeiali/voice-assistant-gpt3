# Voice Chat App (Watson STT/TTS + OpenAI)

## Overview

This is a Flask-based voice-enabled chat application.

Workflow: 1. The browser records user audio. 2. Audio is sent to IBM
Watson Speech-to-Text (lab endpoint) for transcription. 3. The
transcribed text is sent to OpenAI for a short assistant response. 4.
The response text is converted to speech using IBM Watson Text-to-Speech
(lab endpoint). 5. The server returns both text and audio (base64
encoded) to the frontend.

------------------------------------------------------------------------

## Project Structure

-   server.py --- Flask server and API routes
-   worker.py --- Handles Watson STT/TTS and OpenAI calls
-   templates/index.html --- Frontend UI
-   static/script.js --- Client-side JavaScript
-   static/style.css --- Styling
-   requirements.txt --- Python dependencies
-   Dockerfile --- Container configuration

------------------------------------------------------------------------

## Requirements

-   Python 3.10+
-   Docker (optional)
-   OpenAI API key (required)

Note: The Watson endpoints used in this project
(sn-watson-stt.labs.skills.network and
sn-watson-tts.labs.skills.network) are lab services and may only work
inside the Skills Network lab environment.

------------------------------------------------------------------------

## Local Setup

1.  Clone the repository: git clone `<your-repo-url>`{=html} cd
    `<your-project-folder>`{=html}

2.  Install dependencies: pip install -r requirements.txt

3.  Set your OpenAI API key: macOS/Linux: export
    OPENAI_API_KEY="YOUR_API_KEY"

    Windows PowerShell: setx OPENAI_API_KEY "YOUR_API_KEY"

4.  Run the server: python server.py

5.  Open in your browser: http://localhost:8000

------------------------------------------------------------------------

## Run with Docker

Build the image: docker build -t voice-chatapp .

Run the container: docker run -p 8000:8000 -e
OPENAI_API_KEY="YOUR_API_KEY" voice-chatapp

Then open: http://localhost:8000

------------------------------------------------------------------------

## API Endpoints

POST /speech-to-text - Accepts raw audio bytes - Returns: {"text":
"transcribed text"}

POST /process-message - Accepts JSON: {"userMessage": "Hello", "voice":
"default"} - Returns: { "openaiResponseText": "Assistant reply",
"openaiResponseSpeech": "`<base64 encoded wav>`{=html}" }

------------------------------------------------------------------------

## Important Notes

-   Print statements appear in the server terminal or Docker logs, not
    in the browser.
-   Do NOT commit API keys to GitHub.
-   Use environment variables for secrets.
-   Lab-specific certificate configurations are not required in normal
    environments.

------------------------------------------------------------------------

## Security

Never upload: - API keys - Private certificates - Secret tokens

Always use environment variables for sensitive data.
