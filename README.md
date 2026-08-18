# AcornSL

An AI-powered American Sign Language learning companion that combines real-time sign recognition with an on-device LLM for conversational practice and grammar feedback.

https://github.com/user-attachments/assets/80b54a1d-b594-4786-850d-b60da2b781fc


## Overview

AcornSL is a browser-based ASL learning platform designed to make practice accessible, private, and low-pressure.

Users practice ASL through conversations with Acorn, an interactive AI companion. The webcam detects signs in real time and translates them into ASL gloss, while an on-device LLM validates grammar, explains corrections, and keeps the conversation going.

All inference runs locally in the browser, so user data does not need to leave the device.

## Key Features

- **Real-time ASL recognition** — Detects hand signs through the webcam and translates them into ASL gloss
- **AI grammar correction** — Validates ASL grammar and provides explanations for corrections
- **Conversational practice** — Uses the Socratic method to encourage continued practice
- **On-device AI** — Runs LLM inference locally in the browser for privacy and offline use
- **Interactive character** — Acorn's expressions respond dynamically to the conversation
- **Session feedback** — Provides a summary of each practice session with actionable feedback
- **Local chat history** — Saves conversation history locally for later review

## Technical Architecture

AcornSL combines real-time computer vision and on-device LLM pipelines within a React application.

```text
          Webcam
             │
             ▼
      MediaPipe Landmarks
             │
             ▼
   Dynamic Time Warping
             │
             ▼
        ASL Gloss
             │
             ▼
      ┌──────────────┐
      │ On-Device LLM│
      └──────┬───────┘
             │
      ┌──────┴─────────────┐
      ▼                    ▼
Grammar Correction    Conversation
      │                    │
      └─────────┬──────────┘
                ▼
          AcornSL Interface
```

### Computer Vision

The sign recognition pipeline uses **MediaPipe** to extract hand landmarks and **Dynamic Time Warping (DTW)** to compare movement sequences against a custom sign-map database.

This approach supports dynamic whole-word signs rather than limiting recognition to static alphabet signs.

### On-Device LLM

AcornSL uses **Qwen3.5-0.8B** with Transformers.js and ONNX Runtime Web to run inference directly in the browser.

A **four-pipeline architecture** separates ASL grammar correction from conversational response generation, improving the reliability of the small on-device model.

**WebGPU** accelerates inference on compatible hardware to provide responsive conversational interaction while keeping user data on-device.

## Tech Stack

| Category | Technologies |
| --- | --- |
| Frontend | React, Vite |
| Computer Vision | MediaPipe, Dynamic Time Warping |
| LLM | Qwen3.5-0.8B |
| Inference | Transformers.js, ONNX Runtime Web, WebGPU |
| UI | Tailwind CSS, shadcn/ui |
| Design | Figma |

## Engineering Highlights

### Privacy-First AI

All model inference runs locally in the browser, so user data does not need to be sent to a remote server.

### Real-Time Computer Vision

Built a sign recognition pipeline using MediaPipe landmarks and Dynamic Time Warping for dynamic sign matching.

### Multi-Pipeline LLM Architecture

Separated grammar validation, correction, and conversational response generation to improve reliability with a small on-device model.

### WebGPU Acceleration

Used WebGPU-accelerated inference to reduce latency and make on-device AI practical for conversational interaction.

## Running the Code

Install the dependencies:

```bash
npm i
```
Start the development server:

```bash
npm run dev
```
