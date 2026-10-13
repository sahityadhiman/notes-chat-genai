# Chat with Your Notes — AI Study Assistant

> **Paste your notes. Ask questions. Learn from the source.**

Chat with Your Notes is a small generative AI study app. It lets a student paste class notes and ask questions; Google Gemini answers using the provided material and says when it cannot find an answer in the notes.

## 🚀 Live Demo

**Try the app:** [notes-chat-genai.onrender.com](https://notes-chat-genai.onrender.com)

## 📂 GitHub Repository

[github.com/sahityadhiman/notes-chat-genai](https://github.com/sahityadhiman/notes-chat-genai)

---

## 💡 Problem

When studying from long notes, it can be hard to find a specific detail, connect related points, or know whether an answer is actually supported by the material.

### Core Question

**Can a student ask questions about their own notes and get answers grounded in that source?**

## 🎯 Our Solution

The app sends the notes, the current question, and a short window of recent conversation to Gemini. Its prompt asks the model to use only the notes and to say when the answer is missing. Changing the notes starts a fresh chat so an earlier conversation is not carried into a different source.

## 🔄 Study Workflow

1. Paste a focused lesson, chapter section, or set of class notes.
2. Ask a question in the chat box.
3. Read Gemini’s answer alongside the source material.
4. Ask a follow-up question; the app includes recent conversation for context.
5. Clear the chat or replace the notes when you start a new topic.

## ✨ Key Features

### 📚 Notes-Grounded Q&A
Answers are prompted to use the pasted notes and to say when the notes do not contain the answer.

### 💬 Follow-Up Context
The latest conversation turns are included with a question, making follow-ups easier to understand.

### 🔄 Fresh Context for New Notes
The app detects when the notes change and clears the previous chat history.

### 🔐 Bring Your Own Gemini Key
Enter a Gemini API key in the sidebar, or configure a server key for a private deployment. The public demo currently asks each visitor for their own key.

### 🧹 Simple Session Controls
Clear the current conversation at any time. The app does not use a database to save notes or chat history.

## 🧪 Current Prototype

The deployed prototype demonstrates a notes-grounded chat experience using Google Gemini. Notes and chat history are held in the active Streamlit session; they are not stored in an app database. The app is designed for focused study material rather than entire textbooks.

## 🛠️ Technology Stack

- **Python** — application logic
- **Streamlit** — interactive web interface
- **Google Gemini** — language model responses
- **google-genai** — Gemini Python SDK
- **Render** — public web hosting

## 🏗️ Architecture

~~~~text
Student
  │
  ├── Notes + question
  └── Recent chat context
          │
          ▼
Streamlit app (app.py)
          │
          ▼
Google GenAI SDK
          │
          ▼
Gemini model
          │
          ▼
Notes-grounded answer in the chat
~~~~

## 🚀 Run Locally

### Requirements

- Python 3.10 or later
- A Gemini API key from [Google AI Studio](https://aistudio.google.com/app/apikey)

### Windows PowerShell

~~~~powershell
git clone https://github.com/sahityadhiman/notes-chat-genai.git
cd notes-chat-genai
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
$env:GEMINI_API_KEY = "YOUR_GEMINI_API_KEY"
streamlit run app.py
~~~~

### macOS or Linux

~~~~bash
git clone https://github.com/sahityadhiman/notes-chat-genai.git
cd notes-chat-genai
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
export GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
streamlit run app.py
~~~~

You can also paste your key into the app’s password field in the sidebar instead of setting an environment variable. Never commit a real API key to GitHub.

## ⚙️ Configuration

| Variable | Required | Default | Purpose |
|---|---:|---|---|
| `GEMINI_API_KEY` | No, if entered in the sidebar | — | Gemini API key used by the app. A server-configured key is shared by all visitors. |
| `GEMINI_MODEL` | No | `gemini-3.8-flash` | Gemini model name passed to the SDK. |

## ☁️ Deploy on Render

This repository includes a Render Blueprint in `render.yaml`. Create a Blueprint in Render and connect this GitHub repository; Render reads the Blueprint to install the pinned dependencies and start Streamlit.

The public demo is deployed on Render’s free web service. Free services can sleep while idle, so the first visit after inactivity may take about a minute to load. The demo does not have a shared Gemini key configured; visitors enter their own key in the sidebar.

## 🔒 Privacy and Limitations

- When a question is submitted, the notes, question, and recent chat context are sent to Google Gemini to generate an answer.
- A key entered in the public app is sent to the app server for the Gemini request. Use a key only with a deployment you trust.
- The app prompt asks Gemini to stay within the notes, but model output can still be incomplete or incorrect. Check important answers against the original material.
- Do not paste confidential, personal, or sensitive information into the public demo.
- This is a learning prototype, not a persistent note-storage service.
