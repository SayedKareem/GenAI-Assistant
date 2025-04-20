# 🤖 GenAI DevOps WebProject

> A full-stack Generative AI assistant built with FastAPI, OpenAI, and Next.js — containerized using Docker for seamless deployment.

---

## 🌟 Project Overview

**GenAI Assistant** is a full-stack web application designed to:
- Accept user prompts for **interview questions**, **code explanations**, or **DevOps troubleshooting**
- Forward them to a **FastAPI** backend, which communicates with **OpenAI APIs**
- Display AI-generated responses in a **Next.js + Tailwind CSS** frontend

This project showcases a clean separation of UI, backend logic, and AI integration — making it a solid example of a **DevOps-enabled GenAI architecture**.

---

## 🔂️ File Structure Summary

```
GenAI-Assistant/
├── docker-compose.yml           # Compose setup for full-stack app
├── backend/                     # FastAPI + OpenAI integration
│   ├── main.py                  # Entry point for API
│   ├── utils/                   # Business logic: interview, code explainer, DevOps bot
│   ├── Dockerfile
│   ├── requirements.txt
│   └── .env                     # Contains OPENAI_API_KEY (not committed)
├── frontend/                    # Next.js + Tailwind UI
│   ├── pages/                   # Routes: /interview, /explain-code, /devops-assistant
│   ├── components/              # Shared: Navbar, Footer, Layout
│   ├── public/                  # Assets: logos, icons
│   ├── Dockerfile
│   └── tailwind.config.js
```

---

## 🧐 How It Works

### 🔄 Full Flow

```
USER PROMPT → Frontend (Next.js)
→ POST /interview | /explain-code | /devops-assistant → FastAPI (Python)
→ OpenAI API (GPT-3.5/4)
→ Response → UI Rendered with Typing Animation
```

- API key is securely stored in `.env` (not exposed to frontend)
- Requests are handled via `utils/` modules like:
  - `interview.py`
  - `code_explainer.py`
  - `devops_assistant.py`

---

## 🚀 Docker & DevOps Setup

- **Dockerized Full Stack**: Both frontend and backend have individual Dockerfiles
- **Docker Compose** spins everything up:
  - **Backend**: http://localhost:8000
  - **Frontend**: http://localhost:3000
- Internal networking via:
  ```env
  NEXT_PUBLIC_API_BASE_URL=http://backend:8000
  ```

---

## 💻 Available Routes

| Route               | Description                           |
|--------------------|---------------------------------------|
| `/`                | Landing page with animations          |
| `/interview`       | Simulates technical interviews        |
| `/explain-code`    | Explains code using GPT               |
| `/devops-assistant`| Troubleshoots DevOps queries          |

---

## 🧐 Why is this a GenAI DevOps Project?

- Uses **OpenAI LLMs** (GPT-3.5/4) to generate intelligent, human-like responses
- Built with a clean CI/CD-ready architecture
- Seamlessly integrates **DevOps tooling** like Docker & environment separation

---

## 🔐 Secrets & Security

- API keys are managed in `backend/.env`
- Not committed (listed in `.gitignore`)
- Loaded securely using `dotenv` and `os.getenv()`

---

## 📸 Screenshots (optional)

Add screenshots or a short demo here to show off the UI and interaction!

![genAI 1](https://github.com/user-attachments/assets/08e14f84-6766-4403-8631-94c1ccf821eb)
![genAI 2](https://github.com/user-attachments/assets/c63823de-a24d-4563-a642-a20d2f155dbc)
![genAI 3](https://github.com/user-attachments/assets/1bf49b7a-81ba-404f-9a1d-da81da300551)
![genAI 4](https://github.com/user-attachments/assets/1ca381ad-afb8-44da-b95d-d5d9e54b8cc0)

---

## 🛠️ Tech Stack

| Layer         | Tech Used               |
|---------------|--------------------------|
| UI            | Next.js + Tailwind CSS   |
| Backend API   | FastAPI (Python)         |
| LLM Brain     | OpenAI API (GPT-3.5/4)   |
| Infrastructure| Docker + Docker Compose  |

---

## ✨ Get Started

```bash
# Start full-stack app with Docker
docker-compose up --build
```

Then open:
- Frontend → http://localhost:3000
- Backend API → http://localhost:8000


