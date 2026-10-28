# 🥗 NutriGuide — Personalized Nutrition Agentic AI

> A web-based Agentic AI Nutrition Advisor powered by **Meta Llama 3.3 70B Instruct** via **IBM watsonx.ai**

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python)
![Flask](https://img.shields.io/badge/Flask-3.0-lightgrey?logo=flask)
![IBM watsonx](https://img.shields.io/badge/IBM-watsonx.ai-0f62fe?logo=ibm)
![Llama](https://img.shields.io/badge/Meta-Llama%203.3%2070B-purple)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 📌 Overview

**NutriGuide** is a full-stack Agentic AI application that generates personalized, evidence-based nutrition plans using the **Meta Llama 3.3 70B Instruct** model hosted on IBM watsonx.ai. It collects user details (name, age, diet preference, medical history, location), applies AI ethics guardrails, and delivers culturally sensitive, medically aware dietary advice.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🥦 **Personalized 7-Day Plans** | Tailored to age, diet, medical conditions, activity level & goals |
| 💬 **Agentic Q&A Chat** | Real-time nutrition question answering with context awareness |
| 🛡️ **AI Safety Guardrails** | Input + output harmful content detection and blocking |
| ⚖️ **HAM Ethics** | Helpful, Accurate, Mindful tone enforced via prompt engineering |
| 🌏 **Cultural Sensitivity** | Location-aware food recommendations |
| ⚕️ **Medical Disclaimer** | Prominent disclaimer appended to every generated plan |
| 🔒 **Privacy First** | No user data stored — in-memory processing only |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────┐
│          Web Browser — SPA (HTML/CSS/JS)        │
│  Tab 1: Profile Form → Nutrition Plan           │
│  Tab 2: Real-time Chat / Q&A Agent              │
│  Tab 3: About, Ethics & Medical Disclaimer      │
└───────────────────┬─────────────────────────────┘
                    │  REST API (JSON)
┌───────────────────▼─────────────────────────────┐
│           Flask Backend  (app.py)               │
│  /api/generate-plan  — Nutrition Plan Agent     │
│  /api/query          — Q&A Agent                │
│  /api/health         — Health Check             │
│  Guardrail Layer     — Input + Output scan      │
└───────────────────┬─────────────────────────────┘
                    │  ibm-watsonx-ai SDK
┌───────────────────▼─────────────────────────────┐
│  IBM watsonx.ai — AP South (au-syd)             │
│  Model: meta-llama/llama-3-3-70b-instruct       │
└─────────────────────────────────────────────────┘
```

---

## 📁 Project Structure

```
nutrition_ai/
├── app.py                  # Flask backend + IBM watsonx.ai integration
├── requirements.txt        # Python dependencies
├── .gitignore              # Git ignore rules
├── README.md               # This file
└── templates/
    └── index.html          # Single-page web application UI
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

Open your browser at: **[http://localhost:5000](http://localhost:5000)**

---

## 🔌 API Reference

### `POST /api/generate-plan`

Generate a personalized 7-day nutrition plan.

**Request Body:**
```json
{
  "name":           "Priya Sharma",
  "age":            32,
  "diet":           "veg",
  "city":           "Mumbai",
  "country":        "India",
  "medical_history":"Type 2 Diabetes",
  "activity":       "moderate",
  "goals":          "weight_loss"
}
```

**Response:**
```json
{
  "plan":  "## Your Personalized Nutrition Plan...",
  "user":  "Priya Sharma",
  "agent": "NutriGuide — IBM watsonx.ai"
}
```

---

### `POST /api/query`

Ask a nutrition-related question.

**Request Body:**
```json
{
  "query":   "What foods help manage blood pressure?",
  "context": { "name": "Priya", "medical_history": "Hypertension" }
}
```

**Response:**
```json
{
  "answer": "For managing blood pressure, the DASH diet is highly recommended..."
}
```

---

### `GET /api/health`

Returns service status and active model name.

---

## 🛡️ AI Ethics & Guardrails

This application follows responsible AI practices:

- **HAM Principles** — Every prompt enforces a Helpful, Accurate, Mindful tone
- **Input Guardrails** — User inputs are scanned for harmful keywords before being sent to the LLM
- **Output Guardrails** — LLM responses are scanned before being returned to the user
- **No Harmful Advice** — Dangerous diets, self-harm, and unsafe substances are blocked
- **Transparency** — Users are always informed they are interacting with an AI system
- **No Data Retention** — User data is not stored or logged

---

## ⚕️ Medical Disclaimer

> This application and all AI-generated content are provided for **informational and educational purposes only**. They do NOT constitute medical advice, diagnosis, or treatment.
>
> Always consult a qualified healthcare professional — including your physician or a registered dietitian — before making significant dietary changes, especially if you have a medical condition such as diabetes, heart disease, kidney disease, or any chronic illness.
>
> IBM Corporation, its affiliates, and the application developers assume **no liability** for any adverse effects or health consequences resulting from use of this application.

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML5, CSS3, Vanilla JavaScript |
| Backend | Python 3.9+, Flask 3.0 |
| AI Model | Meta Llama 3.3 70B Instruct |
| AI Platform | IBM watsonx.ai (AP South) |
| SDK | ibm-watsonx-ai |

---

## 📄 License

This project is licensed under the **MIT License**.

---

## 🙏 Acknowledgements

- [IBM watsonx.ai](https://www.ibm.com/products/watsonx-ai) for the AI platform
- [Meta AI](https://ai.meta.com/) for the Llama 3.3 model
- IBM Future Developer Program (FDP)
