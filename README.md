# 🚀 Day 9: The Grand Connection - Deploying Local AI to Telegram via Ngrok

## 📌 Project Overview
Today’s mission was to break the AI Agent out of the local environment (`localhost`) and connect it to the real world. I successfully built an end-to-end pipeline where a user can send a message via the Telegram app, the message is tunneled securely to my local n8n instance, processed by the Groq LLM with conversational memory, and the response is sent back to the user instantly.

## ⚙️ Tech Stack & Architecture
* **Ingestion:** Telegram Trigger Node (Webhook)
* **Tunneling:** Ngrok (Reverse Proxy for exposing localhost)
* **Brain & Memory:** n8n AI Agent + Window Buffer Memory + Groq API
* **Action:** Telegram Send Message Node

## 🚧 Challenges Faced & Solutions
1. **Webhook HTTPS Restriction:** Telegram strictly requires HTTPS URLs for webhooks. My local n8n instance was on HTTP. 
   * *Solution:* I deployed **Ngrok** to create a secure tunnel, generating a dynamic HTTPS URL that forwarded traffic directly to port 5678 on my machine.
2. **CLI Database Reset:** Got locked out of the n8n instance locally. 
   * *Solution:* Executed `n8n user-management:reset` via CLI to regain admin access without losing any existing workflow data.
3. **Dynamic Data Mapping:** The AI agent nodes were throwing "no prompt specified" errors.
   * *Solution:* Properly mapped the JSON outputs using expressions (`{{ $json.message.text }}` for the prompt and `chat.id` for routing the return message).
