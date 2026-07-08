# KFAS_LLM_Practice
 
Hands-on practice notebooks for working with language models — from calling a big model over an API, to running a small one locally, to building a retrieval-augmented (RAG) pipeline.
 
Each session is a self-contained Google Colab notebook. No local setup required; a free Google account is enough.
 
---
 
## Sessions
 
| # | Topic | What you do | Open |
|---|-------|-------------|------|
| **1** | **LLM via API** | Call a large model (Gemini) running on Google's servers. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1eStDw_4mMReJoeaASEJBCMO7gjqZVbtA) |
| **2** | **SLM (local)** | Download and run a *small* model *inside* Colab, offline. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1y1_zqLMbv_U_xkwt1ZbQD-AnHg35qa7T) |
| **3** | **RAG** | Combine a retriever with a model to answer from your own documents. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1rKPOUwPyuPMspLTeRc-9NCLZQQeQgeom) |
 
The three sessions build on each other: Sessions 1 and 2 teach the two ways to run a model (remote vs. local), and Session 3 reuses both to build something useful.
 
---
 
## Session 1 — Talking to an LLM through an API
 
Send text to a model on Google's servers and read back its reply — the same way ChatGPT, Copilot, and most AI products work under the hood. You don't download or build anything.
 
By the end you can:
1. Get a **free** Gemini API key and call it from Python.
2. Read a model's response *and* its metadata (tokens used, why it stopped).
3. Control the model with **temperature**, **max output tokens**, and a **system instruction**.
4. Steer answers with **zero-shot** and **few-shot** prompting.
5. Hold a **multi-turn conversation** and stream a reply token-by-token.
Bonus cells cover forcing structured **JSON** output and seeing that an API call is *just an HTTPS request*.
 
## Session 2 — Running a small model locally (SLM)
 
Flip the setup around: download a small model and run it *inside Colab* with no internet call. You meet the same knobs as Session 1 (`temperature`, `max_new_tokens`) and see the quality-vs-cost trade-off first-hand — the model runs on the Colab GPU, weights and all.
 
**API (Session 1) vs Local (Session 2)**
 
| | API | Local |
|---|-----|-------|
| Where the model runs | Google's GPUs | this Colab's GPU |
| Download weights? | No | Yes |
| Quality | Very high | Smaller / weaker |
| Cost | Pay (or free tier) per token | Free, but needs a GPU |
| Works offline / private | No | Yes |
 
## Session 3 — Retrieval-Augmented Generation (RAG)
 
Wire a **retriever** onto a model so it can answer using your own documents instead of only what it memorized during training. Reuses the model-calling skills from Sessions 1–2 and adds retrieval on top.
 
---
 
## Prerequisites
 
- A Google account (any Gmail works).
- For **Session 1**: a free Gemini API key — no credit card, no payment, no Google Cloud project needed. Get one at **[aistudio.google.com/apikey](https://aistudio.google.com/apikey)**.
- For **Sessions 2–3**: switch the Colab runtime to a **GPU** (`Runtime → Change runtime type → GPU`).
## Getting started
 
1. Open a session with its **Open in Colab** badge above.
2. **Make your own copy first: `File → Save a copy in Drive`.** Work in that copy — don't edit the shared notebook directly, so everyone starts from a clean original and your changes stay yours.
3. In your copy, `Runtime → Run all`, or run the cells top to bottom.
4. For Session 1, store your key in **Colab Secrets** (the 🔑 icon) as `GOOGLE_API_KEY` with *Notebook access* on — don't paste keys into shareable cells.
## Storing your API key safely
 
1. Click the **🔑 key icon** in the Colab sidebar.
2. **+ Add new secret**, name it exactly `GOOGLE_API_KEY`, paste the key as the value.
3. Turn on the **Notebook access** toggle.
The notebook reads it from there and falls back to a hidden prompt if it's missing.
 
## Troubleshooting (Session 1)
 
| Symptom | Fix |
|---|---|
| `API key not valid` (400) | Wrong/typo'd key or secret-name mismatch. Recreate the key; confirm the secret is exactly `GOOGLE_API_KEY`. |
| `model ... not found` (404) | Model name changed. Run the list-models cell and use one it prints (drop the leading `models/`). |
| `RESOURCE_EXHAUSTED` (429) | Free-tier rate limit. Wait ~60s and rerun. |
| Empty / `None` response text | Truncated or blocked. Check `response.candidates[0].finish_reason`. |
| `ModuleNotFoundError: google.genai` | Old package clash. Run `!pip uninstall -y google-generativeai`, then re-run the install cell. |
 
---
 
## Tech stack
 
- **Google Gen AI SDK** (`google-genai`) — the modern, unified SDK (the older `google-generativeai` is deprecated).
- **Google Colab** — runtime for all sessions.
- Gemini / Gemma models via the free tier.
## License
 
Add your license of choice here (e.g. MIT).
