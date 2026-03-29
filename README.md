🤖 PerkPilotBot

AI-powered chatbot to discover student discounts and government scholarships using web scraping + LLMs

📌 Project Overview

PerkPilotBot is an end-to-end AI system that automates the discovery of student benefits by combining web scraping, structured storage, and LLM-based querying.

The system collects real-time data from multiple platforms and allows users to interact with it via a command-line chatbot powered by Google Gemini, ensuring responses are accurate and grounded in actual data.

📑 Table of Contents
Project Overview
System Architecture
Project Structure
Features
Technologies Used
Installation
Running the Project
Data Pipeline
Chatbot Workflow
Future Improvements
🧠 System Architecture
Web Sources (UNiDAYS, Student Beans, NSP)
                │
                ▼
        Web Scraping Layer
 (BeautifulSoup + Requests + Selenium)
                │
                ▼
        Data Cleaning & Processing
                │
                ▼
        SQLite Database Storage
   (discounts + scholarships tables)
                │
                ▼
        Prompt Construction Layer
                │
                ▼
     Google Gemini API (LLM)
                │
                ▼
        CLI Chatbot Response
🏗️ Project Structure
PerkPilotBot/
│
├── student_discounts_bot.py      # Main chatbot logic (Gemini integration)
├── web scrape.py                 # Scrapes student discounts
├── govt scholarships scrap.py    # Scrapes scholarships (NSP)
├── student_discounts.db          # SQLite database
├── print database contents.py    # Debug utility
├── websites.txt                  # Source references
└── README.md
✨ Features

✔ End-to-End Data Pipeline (Scraping → Storage → AI Querying)
✔ Multi-source Web Scraping (Static + Dynamic Websites)
✔ AI-powered Chatbot using Gemini API
✔ Structured SQLite Database for fast querying
✔ Strict Data Grounding (No hallucinated responses)
✔ Lightweight CLI-based system
✔ Modular and extensible architecture

⚙️ Technologies Used
💻 Core Technologies
Python
🤖 AI / LLM
Google Gemini API (google-generativeai)
🌐 Web Scraping
BeautifulSoup4
Requests
Selenium
🗄️ Database
SQLite3
⚙️ Tools & Environment
Chrome WebDriver
Google Chrome
⚙️ Installation
Clone the Repository
git clone <your-repo-url>
cd PerkPilotBot
Create Virtual Environment (Recommended)
python -m venv venv

Activate Environment

Windows:

venv\Scripts\activate

Mac/Linux:

source venv/bin/activate
Install Dependencies
pip install -r requirements.txt
Set API Key
# Linux / macOS
export GOOGLE_API_KEY="your_api_key"

# Windows (CMD)
set GOOGLE_API_KEY="your_api_key"

# Windows (PowerShell)
$env:GOOGLE_API_KEY="your_api_key"
▶️ Running the Project
Step 1: Run Scraping Pipeline
python "govt scholarships scrap.py"
python "web scrape.py"
Step 2: Start Chatbot
python student_discounts_bot.py
Step 3: Interaction
Hi Student! Welcome to PerkPilotBot.
What are you looking for?
1) Discounts
2) Government Scholarships/Schemes
🔄 Data Pipeline

The data pipeline performs:

Web scraping from multiple platforms
Data cleaning and structuring
Storage in SQLite database
Retrieval during chatbot execution
🤖 Chatbot Workflow
Load dataset from database
Ask user intent (Discounts / Scholarships)
Construct contextual prompt
Send to Gemini (gemini-1.5-flash)
Generate response strictly based on stored data
🚀 Future Improvements
🌐 Web application (Flask / FastAPI)
🔎 Semantic search with vector DB (FAISS / Pinecone)
⏱️ Automated scheduled scraping
🗄️ Migration to PostgreSQL / MongoDB
📊 Ranking & filtering system
📱 UI-based interface
👨‍💻 Author

Kumar Harsh
