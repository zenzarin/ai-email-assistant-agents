# AI Email Assistant with Agents & Smart Routing (n8n + Ollama)

An advanced n8n automation that reads incoming Gmail messages, uses AI agents to extract structured information, routes emails by category with a Switch node, checks Google Sheets for existing records, and drafts context-aware replies — all powered by locally hosted LLMs.

Built during the Digital Marketing course (B3E4500101) at Tokyo International University. This is the extended version of my basic email classifier.

<img width="2556" height="1392" alt="email-agents-workflow png" src="https://github.com/user-attachments/assets/93a2f367-0927-49d3-9576-b4ea42dd995c" />


## What it does

1. **Gmail Trigger** — fires on every new email
2. **AI Agent + Structured Output Parser** — extracts structured data from the email (category, intent, customer details) as validated JSON
3. **Switch node** — routes each email down a different branch based on its category
4. **Google Sheets lookup** — checks whether the sender/case already exists before deciding to append or update a row
5. **Second AI Agent** — writes a context-aware reply using the extracted details
6. **Gmail draft** — the reply is saved as a draft for human review before sending

## Tech stack

- **n8n** (self-hosted on a VPS with Docker + Caddy)
- **Ollama** running qwen2.5 locally — zero API costs
- **n8n AI Agent nodes** with system prompts and JSON Schema output parsing (auto-fix enabled)
- **Switch node** for multi-branch routing
- **Gmail API** and **Google Sheets API** (OAuth2)
- **JavaScript Code nodes** for text cleaning and data shaping

## Skills demonstrated

- Chaining multiple AI agents in one pipeline (extract → route → generate)
- Structured information extraction with JSON Schema validation
- Conditional routing and lookup-before-write logic (append vs. update)
- Human-in-the-loop automation design
- Prompt engineering for small local models

## How to run

1. Import `email-assistant-advanced.json` into an n8n instance (v1.60+)
2. Connect your own Gmail OAuth2 and Google Sheets OAuth2 credentials
3. Point the Ollama nodes at your Ollama server and pull a model, e.g. `ollama pull qwen2.5:1.5b`
4. Replace `YOUR_SPREADSHEET_ID` in the Sheets nodes with your own sheet
5. Activate the workflow

<img width="2550" height="1338" alt="Screenshot 2026-07-15 202838" src="https://github.com/user-attachments/assets/74ac5b0a-6c1c-4abe-8450-137627b853b1" />

