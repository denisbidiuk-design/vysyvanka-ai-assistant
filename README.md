# <div style="padding:12px; background:#1e1e1e; color:#fff; border-radius:8px;">VYSHYVANKA AI Assistant — Project Overview</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
The VYSHYVANKA AI Assistant is a production‑ready conversational system designed to support customers of the VYSHYVANKA embroidered clothing store.  
The project integrates a Telegram bot, Google Sheets logging, Gemini 2.5 Flash LLM, and a modular Python backend.  
The assistant helps users choose embroidered shirts, provides product information, and ensures safe, controlled responses without hallucinations.

The system is built with clean architecture principles, full type annotations, English documentation, and a clear separation of concerns across modules.
</div>

---

## <div style="padding:8px; background:#f0f0f0; border-left:6px solid #d0021b;">1. API Keys & Required Setup</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">

### 🔑 GEMINI_API_KEY — Create Gemini API Key  
To generate your Gemini API key, open the official Google AI Studio:  
👉 https://aistudio.google.com/app/apikey

You will receive a key like:  
`AIzaSyXXXXXX...`

---

### 🤖 TELEGRAM_TOKEN — Create Telegram Bot Token  
To create a Telegram bot token, open **BotFather** in Telegram:  
👉 https://t.me/BotFather

Steps:  
1. Open BotFather  
2. Send `/newbot`  
3. Choose bot name  
4. Choose bot username  
5. Receive your token:  
   `1234567890:ABCDEF...`

---

### 📄 CREDENTIALS_FILE — Create Google Service Account JSON  
To generate your Google Cloud service account credentials:  
👉 https://console.cloud.google.com/iam-admin/serviceaccounts

Steps:  
1. Create a new Service Account  
2. Assign role: **Editor** or **Sheets API Editor**  
3. Click **Keys → Add Key → JSON**  
4. Download the file:  
   `my-project-XXXXXX.json`

---

### 📊 SPREADSHEET_ID — Create Google Sheets Document  
To create a Google Sheets file:  
👉 https://sheets.google.com

Steps:  
1. Create a new sheet  
2. Open the URL  
3. Copy the ID from the link:  
   Example:  
   `https://docs.google.com/spreadsheets/d/14uSRhTsKUFlq_EuOGUjLiZrjApStOU/edit`  
   Your ID is:  
   `14uSRhTsKUFlq_EuOGUjLiZrjApStOU`

</div>

---

## <div style="padding:8px; background:#f0f0f0; border-left:6px solid #4a90e2;">2. Project Goals</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
<ul>
<li>Provide customers with accurate, friendly, and helpful product guidance</li>
<li>Avoid hallucinations by strictly following a curated knowledge base</li>
<li>Maintain safe and controlled communication</li>
<li>Log all conversations for analytics and quality control</li>
<li>Operate reliably as a Telegram bot</li>
<li>Use a modular, maintainable Python codebase suitable for production deployment</li>
</ul>
</div>

---

## <div style="padding:8px; background:#f0f0f0; border-left:6px solid #7ed321;">3. System Architecture</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
The project follows a modular architecture, where each component is isolated into its own Python module.  
This improves maintainability, readability, and scalability.
</div>


project/
│
├── main.py
├── config.py
├── config_example.py
│
├── system_prompt_en.md
├── hallucination_tests_en.md
│
└── utils/
├── sheets.py
├── telegram.py
└── gemini.py

### <div style="padding:6px; background:#fafafa; border-left:4px solid #50e3c2;">Module Responsibilities</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
<b>config.py</b> — Stores API keys, file paths, and constants.  
<b>prompt_loader.py</b> — Loads the system prompt and hallucination test cases from files.  
<b>gemini_client.py</b> — Wraps the Gemini 2.5 Flash API and handles prompt construction.  
<b>sheets_logger.py</b> — Logs all conversations to Google Sheets with timestamps.  
<b>validator.py</b> — Validates user input to prevent unsafe characters and injection attacks.  
<b>telegram_api.py</b> — Handles communication with the Telegram Bot API.  
<b>bot.py</b> — Main bot logic: message processing, validation, LLM calls, logging.  
<b>main.py</b> — Entry point that starts the Telegram bot.
</div>

---

## <div style="padding:8px; background:#f0f0f0; border-left:6px solid #bd10e0;">4. Core Features</div>

### <div style="padding:6px; background:#fafafa; border-left:4px solid #4a90e2;">4.1 AI‑Driven Customer Assistance</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
The assistant uses Gemini 2.5 Flash to generate responses based on a strict system prompt.  
It supports:
<ul>
<li>Product recommendations</li>
<li>Size guidance</li>
<li>Delivery and payment information</li>
<li>Accessory suggestions</li>
<li>Clarifying questions</li>
<li>Customer intent classification</li>
</ul>
All responses follow strict formatting rules and avoid hallucinations.
</div>

### <div style="padding:6px; background:#fafafa; border-left:4px solid #d0021b;">4.2 Hallucination Prevention Layer</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
The system includes a dedicated hallucination test suite appended to the system prompt.  
This ensures the model:
<ul>
<li>Does not invent discounts</li>
<li>Does not guess materials or origins</li>
<li>Does not assume availability</li>
<li>Does not comment on competitors</li>
<li>Does not promise delivery times</li>
<li>Does not confirm unverified claims</li>
</ul>
This layer dramatically improves reliability.
</div>

### <div style="padding:6px; background:#fafafa; border-left:4px solid #f5a623;">4.3 Telegram Bot Integration</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
<ul>
<li>Receives messages via Telegram API</li>
<li>Processes them through the LLM</li>
<li>Sends structured replies</li>
<li>Logs all interactions</li>
</ul>
Runs in an infinite loop with safe error handling.
</div>

### <div style="padding:6px; background:#fafafa; border-left:4px solid #7ed321;">4.4 Google Sheets Logging</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
Every interaction is logged with:
<ul>
<li>Timestamp</li>
<li>User ID</li>
<li>User message</li>
<li>Bot reply</li>
</ul>
This enables:
<ul>
<li>Analytics</li>
<li>Quality control</li>
<li>Debugging</li>
<li>Customer behavior tracking</li>
</ul>
</div>

### <div style="padding:6px; background:#fafafa; border-left:4px solid #50e3c2;">4.5 Input Validation & Security</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
Validator ensures messages contain only:
<ul>
<li>English letters</li>
<li>Cyrillic letters</li>
<li>Digits</li>
<li>Spaces</li>
<li>Dash</li>
<li>Comma</li>
<li>Period</li>
<li>Apostrophe</li>
</ul>
This prevents:
<ul>
<li>SQL injection</li>
<li>Script injection</li>
<li>Unicode exploits</li>
<li>Emoji spam</li>
</ul>
</div>

---

## <div style="padding:8px; background:#f0f0f0; border-left:6px solid #4a90e2;">5. System Prompt Design</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
The system prompt defines:
<ul>
<li>Tone and style</li>
<li>Customer categories</li>
<li>Response structure</li>
<li>Product catalog</li>
<li>Restrictions</li>
<li>Safety rules</li>
<li>Hallucination prevention</li>
</ul>
It ensures the assistant behaves like a professional store consultant.
</div>

---

## <div style="padding:8px; background:#f0f0f0; border-left:6px solid #7ed321;">6. Technology Stack</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
<b>Language:</b> Python 3  
<b>AI Model:</b> Gemini 2.5 Flash  
<b>Bot Platform:</b> Telegram Bot API  
<b>Logging:</b> Google Sheets API  
<b>Environment:</b> Google Colab / Any Python runtime  
<b>Architecture:</b> Modular, production‑ready  
</div>

---

## <div style="padding:8px; background:#f0f0f0; border-left:6px solid #bd10e0;">7. Key Strengths</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
<ul>
<li>Clean, maintainable architecture</li>
<li>Fully documented in English</li>
<li>Strong hallucination control</li>
<li>Real‑time logging</li>
<li>Secure input validation</li>
<li>Easy to extend (database, admin panel, analytics)</li>
<li>Ready for deployment on server or cloud</li>
</ul>
</div>

---

## <div style="padding:8px; background:#f0f0f0; border-left:6px solid #f5a623;">8. Future Enhancements</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
<ul>
<li>Docker containerization</li>
<li>.env configuration support</li>
<li>Admin dashboard for logs</li>
<li>Product database instead of static prompt</li>
<li>Rate‑limit handling for Gemini</li>
<li>Unit tests for each module</li>
<li>Multi‑language support</li>
</ul>
</div>

---

## <div style="padding:8px; background:#f0f0f0; border-left:6px solid #4a90e2;">9. Summary</div>

<div style="padding:12px; border:1px solid #ddd; border-radius:6px;">
The VYSHYVANKA AI Assistant is a robust, production‑grade conversational system designed with reliability, safety, and maintainability in mind.  
Its modular architecture, strict prompt engineering, and integrated logging make it suitable for real business use.
</div>




---
