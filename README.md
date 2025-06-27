# FreeScribe — ML-Powered Transcription & Translation Web App

![Screenshot 2024-09-06 at 16 57 25](https://github.com/user-attachments/assets/d6d0c53e-5b3e-4d49-b6e8-1dfbc6808a0f) ![Screenshot 2024-09-06 at 16 57 51](https://github.com/user-attachments/assets/ce94c628-8103-44d0-ae0e-4f7dc184f404) ![Screenshot 2024-09-06 at 16 58 10](https://github.com/user-attachments/assets/794bde3c-d08d-43cc-9e49-eb44033fe4a6) ![Screenshot 2024-09-06 at 16 58 17](https://github.com/user-attachments/assets/3ae53a9c-7908-4e09-bdbf-0e922a436789) ![Screenshot 2024-09-06 at 16 58 30](https://github.com/user-attachments/assets/77398251-b28d-4194-a27c-52690589d3bf) ![Screenshot 2024-09-06 at 16 58 48](https://github.com/user-attachments/assets/cf804485-b6ad-4fa3-8040-9a26fe7845b9) ![Screenshot 2024-09-06 at 16 59 46](https://github.com/user-attachments/assets/98b2b40f-d2fc-4c03-bead-d80b91fc1ed9)

---

## Project Summary

**FreeScribe** is a modern, open-source transcription and translation web application that leverages on-device machine learning models, running entirely in your browser using Web Workers. Users can record or upload audio, transcribe speech to text, translate between languages, and export the results — all with privacy and speed, without sending data to any backend server.

- **Live demo:** [https://free-scribe-arnob.vercel.app/](https://free-scribe-arnob.vercel.app/)
---

## Table of Contents

- [Project Summary](#project-summary)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
  - [Web Worker Architecture](#web-worker-architecture)
  - [Machine Learning Model](#machine-learning-model)
- [Getting Started](#getting-started)
  - [Installation](#installation)
  - [Running Locally](#running-locally)
- [Usage Walkthrough](#usage-walkthrough)
- [Teaching Content & Examples](#teaching-content--examples)
- [Keywords](#keywords)
- [Conclusion](#conclusion)
- [License](#license)

---

## Features

- 🎙️ **Audio Input:** Record live or upload MP3/WAV files for transcription.
- ✍️ **Transcription:** Converts speech to text using ML models (OpenAI Whisper).
- 🌎 **Translation:** Translate transcribed text into multiple languages.
- ⚡ **Runs Locally:** All ML inference runs in-browser via Web Workers for privacy and speed.
- 💾 **Export:** Download or copy the resulting text.
- 🚀 **Modern UI:** Built with React, Vite, and TailwindCSS.
- 💡 **No Cost:** 100% free and open-source.

---

## Technology Stack

- **Frontend:** React 18, Vite, TailwindCSS
- **Web Worker ML:** [`@xenova/transformers`](https://github.com/xenova/transformers.js)
- **Transcription Model:** OpenAI Whisper (via transformers.js)
- **Other:** ESLint, PostCSS, modern ES2020+ JavaScript

---

## Project Structure

```
/
├── public/
│   └── vite.svg           # App icon
├── src/
│   ├── components/
│   │   ├── Header.jsx     # Top navigation and branding
│   │   ├── Footer.jsx     # Footer
│   │   ├── HomePage.jsx   # Landing/upload UI
│   │   ├── FileDisplay.jsx# Audio file display and controls
│   │   ├── Information.jsx# Output display
│   │   └── Transcribing.jsx # Loading/transcribing UI
│   ├── utils/
│   │   ├── presets.js     # Worker message types, language codes, model names
│   │   └── whisper.worker.js # Main ML Web Worker logic
│   ├── App.jsx            # Main application logic
│   ├── main.jsx           # Entry point
│   └── index.css          # Tailwind and custom styles
├── index.html             # HTML template
├── package.json           # Dependencies & scripts
└── ... (config files)
```

---

## How It Works

### Web Worker Architecture

- The app delegates heavy ML inference to a **Web Worker** (`whisper.worker.js`). This prevents UI blocking and ensures smooth user experience.
- The worker receives audio data, loads the ML model (Whisper), and performs transcription/translation asynchronously.
- Communication uses structured messages (see `presets.js` for message types).

### Machine Learning Model

- **Transcription** uses the *OpenAI Whisper* model, via `@xenova/transformers`, running entirely in-browser (no server needed).
- **Translation** is performed using Whisper’s multilingual capabilities and language codes defined in `presets.js`.
- Model progress and results are streamed back to the main app for display.

---

## Getting Started

### Installation

1. **Clone the repo:**
   ```bash
   git clone https://github.com/arnobt78/FreeScribe-Transcription-Translation-ML-App--ReactVite.git
   cd FreeScribe-Transcription-Translation-ML-App--ReactVite
   ```

2. **Install Node.js:**  
   Download and install from [nodejs.org](https://nodejs.org/en/).

3. **Install dependencies:**
   ```bash
   npm install
   ```

4. **Install Transformers.js:**
   ```bash
   npm i @xenova/transformers
   ```

### Running Locally

Start the development server:
```bash
npm run dev
```
Open [http://localhost:5173/](http://localhost:5173/) in your browser.

---

## Usage Walkthrough

1. **Home Screen:**  
   Select to record audio or upload an MP3/WAV file.

2. **Audio Processing:**  
   Once uploaded or recorded, the file is displayed. Click "Transcribe" to start.

3. **ML Inference:**  
   The app loads the Whisper model in a web worker and processes your audio.

4. **View & Translate:**  
   The transcribed text appears. Use translation options to convert it into another language.

5. **Export or Copy:**  
   Download the text as a file or copy it to your clipboard.

---

## Teaching Content & Examples

### Example: Adding a New Language

To add a new translation language, extend the `LANGUAGES` object in `src/utils/presets.js`:

```javascript
export const LANGUAGES = {
  ...,
  "Spanish": "spa_Latn",
  // Add more as needed
};
```

### Example: Using the Web Worker

The worker is initialized in `App.jsx`:

```javascript
worker.current = new Worker(new URL('./utils/whisper.worker.js', import.meta.url), { type: 'module' });
worker.current.postMessage({
  type: MessageTypes.INFERENCE_REQUEST,
  audio,
  model_name: 'openai/whisper-tiny.en'
});
```

The worker receives audio, runs the model, and sends back results via `postMessage`.

---

## Keywords

- Transcription
- Translation
- Machine Learning
- React
- Vite
- TailwindCSS
- Web Worker
- OpenAI Whisper
- Speech Recognition
- @xenova/transformers
- In-browser ML
- Audio Processing

---

## Conclusion

FreeScribe streamlines advanced speech-to-text and language translation—directly in your browser, for free. Powered by modern frontend tools and the latest open-source ML models, it’s a practical, privacy-respecting alternative to expensive SaaS solutions.

---

## License

MIT License. © 2030 [arnobt78](https://github.com/arnobt78)

---
