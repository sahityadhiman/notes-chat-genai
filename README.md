# Chat with Your Notes

A small GenAI study app. Paste class notes and ask questions; Gemini answers from the notes and says when the answer is not there.

## Run locally

You need Python 3.10 or later and a Gemini API key. Create a key in [Google AI Studio](https://aistudio.google.com/app/apikey).

Open PowerShell in this folder and run:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m streamlit run app.py
```

Paste your API key into the app's sidebar. You can also set `GEMINI_API_KEY` in PowerShell before launching. Never commit an API key to GitHub.

## How it works

The app sends the notes, recent chat, and question to Gemini with instructions to answer only from the notes. It uses Streamlit for the interface and Google's `google-genai` Python package for model calls.

To use a different Gemini model, set `GEMINI_MODEL` in the shell before launching. The default is `gemini-3.8-flash`.

## Deploy on Render

This repository includes a Render Blueprint. In Render, create a new Blueprint and connect this GitHub repository; Render will build and launch the app using the settings in `render.yaml`. The free web service can sleep after inactivity, so its first request may take about a minute to load.

The public app asks visitors to enter their own Gemini API key. If you configure `GEMINI_API_KEY` in Render instead, all visitors share that key's quota. Keep the key in Render's environment settings, never in this repository.

**Privacy:** Notes and questions are sent to Google's Gemini API when you ask a question. Avoid private or sensitive text.
