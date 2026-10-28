# 📱 SocialMind — Social Media Agentic AI

> A full-stack Agentic AI Social Media application powered by **IBM Granite 13B Instruct v2** via **IBM watsonx.ai**

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python)
![Flask](https://img.shields.io/badge/Flask-3.0-lightgrey?logo=flask)
![IBM watsonx](https://img.shields.io/badge/IBM-watsonx.ai-0f62fe?logo=ibm)
![IBM Granite](https://img.shields.io/badge/IBM-Granite%2013B-6929c4?logo=ibm)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 📌 Overview

**SocialMind** is a full-stack Agentic AI Social Media application that generates personalized social media content, performs trend analysis, provides an interactive analytics dashboard, and includes an AI-powered chatbot — all powered by **IBM Granite 13B Instruct v2** on IBM watsonx.ai.

The application collects brand details (name, industry, target audience, platforms, tone, goals, competitors) and delivers complete social media content packages including posts, captions, hashtags, content calendars, and posting schedules.

---

## ✨ Features

| Feature | Description |
|---|---|
| 📦 **Content Package Generator** | 5 platform-specific posts, hashtag strategy, 7-day content calendar, competitor insights |
| 📈 **Trend Analysis Agent** | Industry trends, sentiment analysis, viral content formats, emerging hashtags |
| 📊 **Analytics Dashboard** | Interactive charts for engagement, sentiment, content performance (AI-estimated) |
| ⚡ **Post Optimizer** | Rewrite and improve existing posts for specific platforms |
| 🖼️ **Caption from Image** | Generate 3 caption styles from a text description of an image |
| 💬 **AI Chatbot** | Real-time social media Q&A with brand context awareness |
| ✅ **Human Approval Queue** | All AI-generated content requires human review before publishing |
| 🛡️ **Ethical AI Guardrails** | Input + output harmful content detection and blocking |
| ⚖️ **HAM Ethics** | Helpful, Accurate, Mindful tone enforced via prompt engineering |
| 🔒 **Privacy First** | PII redaction active; no user data stored |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│             Web Browser — SPA (HTML/CSS/JS)             │
│  Tab 1: Generate Content Package                        │
│  Tab 2: Trend Analysis                                  │
│  Tab 3: Analytics Dashboard (Chart.js)                  │
│  Tab 4: Post Optimizer + Image Captions                 │
│  Tab 5: AI Chatbot                                      │
│  Tab 6: Human Approval Queue                            │
│  Tab 7: About & Disclaimer                              │
└────────────────────────┬────────────────────────────────┘
                         │  REST API (JSON)
┌────────────────────────▼────────────────────────────────┐
│                 Flask Backend (app.py)                  │
│  /api/generate-content    — Content Package Agent       │
│  /api/analyze-trends      — Trend Analysis Agent        │
│  /api/chatbot             — Q&A Agent                   │
│  /api/optimize-post       — Post Optimizer              │
│  /api/caption-from-image  — Caption Writer              │
│  /api/analytics/dashboard — Analytics Data              │
│  /api/approvals           — Approval Queue              │
│  Guardrail Layer          — Input + Output scan         │
│  PII Redaction            — Email/phone sanitization    │
└────────────────────────┬────────────────────────────────┘
                         │  ibm-watsonx-ai SDK
┌────────────────────────▼────────────────────────────────┐
│  IBM watsonx.ai — AP South (au-syd)                     │
│  Model: ibm/granite-13b-instruct-v2                     │
└─────────────────────────────────────────────────────────┘
```

---

## 📁 Project Structure

```
social_media_ai/
├── app.py                  # Flask backend + IBM watsonx.ai + all agents
├── requirements.txt        # Python dependencies
├── .gitignore              # Git ignore rules
├── README.md               # This file
└── templates/
    └── index.html          # Single-page web application (7 tabs)
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9 or higher
- pip
- An IBM watsonx.ai account with API access

### 1. Clone the Repository

```bash
git clone https://github.com/ManasiWalke/test.git
cd test
```

### 2. Create a Virtual Environment

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS / Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the project root:

```env
IBM_API_KEY=your_ibm_api_key_here
IBM_PROJECT_ID=your_project_id_here
IBM_ENDPOINT_URL=https://au-syd.ml.cloud.ibm.com
```

> ⚠️ **Never commit your `.env` file.** It is listed in `.gitignore`.

### 5. Run the Application

```bash
python app.py
```

Open your browser at: **[http://localhost:5001](http://localhost:5001)**

---

## 🔌 API Reference

### `POST /api/generate-content`

Generate a complete social media content package.

**Request Body:**
```json
{
  "brand_name":  "Nexora Tech",
  "industry":    "Technology",
  "audience":    "Millennials and Gen Z tech enthusiasts",
  "platforms":   ["Instagram", "LinkedIn", "Twitter/X"],
  "tone":        "Friendly & Casual",
  "goals":       "Brand Awareness",
  "campaign":    "Summer Product Launch",
  "competitor":  "TechRival Inc"
}
```

**Response:**
```json
{
  "content":     "## Social Media Content Package...",
  "brand":       "Nexora Tech",
  "approval_id": 1,
  "agent":       "SocialMind — IBM Granite AI",
  "status":      "pending_approval"
}
```

---

### `POST /api/analyze-trends`

Analyze social media trends for an industry.

**Request Body:**
```json
{
  "industry":  "Technology",
  "platforms": ["Instagram", "LinkedIn", "Twitter/X"]
}
```

---

### `POST /api/chatbot`

Ask a social media strategy question.

**Request Body:**
```json
{
  "query":   "What are the best posting times for LinkedIn?",
  "context": { "brand_name": "Nexora Tech", "industry": "Technology" }
}
```

---

### `POST /api/optimize-post`

Optimize an existing post for a platform.

**Request Body:**
```json
{
  "post":     "Check out our new product. It is great. Buy now.",
  "platform": "Instagram",
  "tone":     "Friendly & Casual"
}
```

---

### `POST /api/caption-from-image`

Generate captions from an image description.

**Request Body:**
```json
{
  "description": "A team of diverse professionals celebrating around a laptop",
  "brand": { "brand_name": "Nexora Tech", "tone": "Inspirational" }
}
```

---

### `POST /api/analytics/dashboard`

Get simulated analytics data.

**Request Body:**
```json
{
  "brand_name": "Nexora Tech",
  "platforms":  ["Instagram", "LinkedIn", "Twitter/X"]
}
```

---

### `GET /api/approvals`

Get all items in the human approval queue.

---

### `PATCH /api/approvals/<id>`

Approve or reject a content item.

**Request Body:**
```json
{ "action": "approve" }
```

---

### `GET /api/health`

Returns service status and active model.

---

## 🛡️ AI Ethics & Guardrails

| Safeguard | Implementation |
|---|---|
| **HAM Principles** | Every prompt enforces Helpful, Accurate, Mindful tone |
| **Input Guardrails** | User inputs scanned for harmful/inappropriate content |
| **Output Guardrails** | LLM responses scanned before being returned |
| **Human Approval** | All generated content enters an approval queue |
| **PII Redaction** | Email addresses and phone numbers auto-redacted from outputs |
| **AI Transparency** | All metrics clearly labelled as AI estimates |
| **No Data Retention** | User data is not stored or logged |
| **Ethical Blocking** | Hate speech, spam, misinformation requests blocked |

---

## ⚠️ Disclaimer

> All AI-generated content, engagement metrics, trend predictions, and analytics are **AI-estimated simulations** — not real-time platform data.
>
> This application is for **informational and creative assistance only**. Human review and approval is required before publishing any AI-generated content.
>
> IBM Corporation, its affiliates, and the application developers assume **no liability** for any business outcomes.

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML5, CSS3, Vanilla JavaScript, Chart.js |
| Backend | Python 3.9+, Flask 3.0 |
| AI Model | IBM Granite 13B Instruct v2 |
| AI Platform | IBM watsonx.ai (AP South — au-syd) |
| SDK | ibm-watsonx-ai |

---

## 📄 License

This project is licensed under the **MIT License**.

---

## 🙏 Acknowledgements

- [IBM watsonx.ai](https://www.ibm.com/products/watsonx-ai) for the AI platform
- [IBM Granite](https://www.ibm.com/granite) for the LLM
- IBM Future Developer Program (FDP)
- [Chart.js](https://www.chartjs.org/) for data visualisation
