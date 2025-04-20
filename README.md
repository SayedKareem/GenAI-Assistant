 Project Overview: GenAI Assistant
OPEN_API_KEY: sk-svcacct-d
GenAI Assistant is a full-stack application designed to:
• Accept user prompts for interview questions, code explanations, or DevOps help
• Send them to a backend built with FastAPI
• The backend talks to OpenAI for responses
• A frontend (Next.js + Tailwind CSS) provides a beautiful interactive UI
==================================
 File Structure Summary
GenAI-Assistant-main/
├── docker-compose.yml
├── backend/ # FastAPI + OpenAI integration
│ ├── main.py
│ ├── utils/ # Functional logic (code explainer, interview bot, devops assistant)
│ ├── Dockerfile
│ ├── requirements.txt
│ └── .env # OPENAI_API_KEY lives here
├── frontend/ # Next.js + Tailwind UI
│ ├── pages/ # Each route = individual page (interview, explain-code, etc.)
│ ├── components/ # Navbar, Footer, Layout shared
│ ├── public/ # yt.svg, li.svg, logo assets
│ ├── Dockerfile
│ ├── tailwind.config.js
│ └── postcss.config.js
=======================================
 Backend (FastAPI)
 File: backend/main.py
This is the entrypoint for the FastAPI server.
• Loads OPENAI_API_KEY from .env
• Configures CORS so frontend can call it
• Defines 3 API endpoints:
  o POST /interview
  o POST /explain-code
  o POST /devops-assistant
======================================

Each one uses logic from:
backend/utils/
├── interview.py
├── code_explainer.py
├── devops_assistant.py
 Example: utils/interview.py
from openai import OpenAI
def handle_interview(question: str):
 client = OpenAI()
 response = client.chat.completions.create(
 model="gpt-3.5-turbo",
 messages=[{"role": "user", "content": question}]
 )
 return response.choices[0].message.content
 Similar structure is used for all utilities. This decouples business logic from the API layer.

==================================
 Frontend (Next.js + TailwindCSS)
 **Pages (Routes)**
Each file in pages/ is a route in your app:
File                 Route             Purpose
index.js               /              Landing page with animations
interview.js           /              interview UI to ask interview questions
explain-code.js       /               explain-code Paste code and get GPT explanation
devops-assistant.js   /               devops-assistant Troubleshoot DevOps issues with LLM
 **Components:**
File Purpose
Navbar.js Top fixed navigation with links/icons
Footer.js Social icons + copyright
Layout.js Wraps each page with shared Navbar/Footer
==========================

Used in _app.js:
import Layout from '../components/Layout'
export default function App({ Component, pageProps }) {
 return (
 <Layout>
 <Component {...pageProps} />
 </Layout>
 );
} 
================================

 Secrets & API Key Flow
• .env in backend/ stores the OPENAI_API_KEY
• It's not committed to GitHub (ignored in .gitignore) • Loaded into FastAPI via dotenv → os.getenv("OPENAI_API_KEY")
• Frontend never sees the API key — it only sends questions to backend

===================================

 Full Flow: User to OpenAI
USER TYPES PROMPT IN UI
 ↓
FRONTEND SENDS POST TO: HTTP://LOCALHOST:8000/<ROUTE>
 ↓
FASTAPI RECEIVES → PARSES FORM → CALLS OPENAI API
 ↓
OPENAI GENERATES RESULT
 ↓
FASTAPI SENDS RESPONSE BACK TO FRONTEND
 ↓
FRONTEND DISPLAYS IT WITH TYPING ANIMATION 

========================

 Docker & Compose
  • Backend & frontend both have their own Dockerfile
  • docker-compose.yml spins up both:
    o Backend on http://localhost:8000
    o Frontend on http://localhost:3000
  • Frontend accesses backend via internal Docker DNS:
env
NEXT_PUBLIC_API_BASE_URL=http://backend:8000
====================
 Why Is This a GenAI Project?
  • It uses LLMs (OpenAI) for:
        o Simulating interviews
        o Explaining code
        o Troubleshooting DevOps content
  • Prompts → LLM → Answers → Dynamic UI
  • Clean frontend + API separation = ideal GenAI project structure
  ======================================

 Recap
Layer                                       Tech Used                         Purpose
UI                                     Next.js + Tailwind             Interactive interface
Backend API                             FastAPI + Python            Handles requests, integrates OpenAI
LLM Brain                             OpenAI (GPT-3.5/4)             Generates intelligent responses
Infra                                 Docker + Compose             Containerization, portability  
======================**END**=============================
