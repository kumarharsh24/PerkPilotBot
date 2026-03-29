PerkPilotBot 🤖

PerkPilotBot is a command-line AI chatbot designed to help students discover relevant discounts and government scholarships. It leverages web scraping techniques and integrates with the Google Gemini API to provide intelligent, data-driven responses.

🚀 Overview

PerkPilotBot automates the process of collecting and querying student benefits by:

Scraping data from multiple trusted platforms
Storing structured data locally in a SQLite database
Using an LLM (Gemini) to generate contextual responses based strictly on collected data
⚙️ System Architecture

The project operates in two primary phases:

1. Data Collection (Web Scraping)
Python scripts extract data from various sources:
MyUNIDAYS → via requests and BeautifulSoup
Student Beans → via Selenium (handles dynamic content)
National Scholarship Portal (India) → scholarship data extraction
Scripts involved:
web scrape.py → collects student discounts
govt scholarships scrap.py → collects government scholarships
Data Processing:
Cleaned and structured before storage
Stored in student_discounts.db (SQLite database)
Database Schema:
discounts table
govt_scholarships table
2. Chatbot Interaction (AI Layer)
Main script: student_discounts_bot.py

Workflow:

Loads data from SQLite database
Prompts user to choose:
Discounts
Scholarships
Constructs a dynamic prompt including relevant dataset
Sends prompt to Gemini (gemini-1.5-flash)
Returns a response constrained strictly to available data
🛠️ Tech Stack
Component	Technology Used
AI Model	Google Gemini API (google-generativeai)
Web Scraping	Selenium, BeautifulSoup4, Requests
Database	SQLite3
Programming	Python
📁 Project Structure
PerkPilotBot/
│
├── student_discounts_bot.py     # Main chatbot script
├── web scrape.py                # Scrapes student discounts
├── govt scholarships scrap.py   # Scrapes government scholarships
├── student_discounts.db         # SQLite database (generated after scraping)
├── print database contents.py   # Debugging utility
├── websites.txt                 # Source URLs reference
└── README.md                    # Project documentation
⚙️ Setup Instructions
1. Prerequisites

Ensure the following are installed:

Python 3.x
Google Chrome
Chrome WebDriver (matching your Chrome version)
2. Installation

Clone the repository:

git clone <your-repo-url>
cd PerkPilotBot

Create a requirements.txt file:

google-generativeai
requests
beautifulsoup4
selenium

Install dependencies:

pip install -r requirements.txt
3. Configure API Key

Set your Google Gemini API key as an environment variable:

macOS/Linux:

export GOOGLE_API_KEY="your_api_key_here"

Windows (Command Prompt):

set GOOGLE_API_KEY="your_api_key_here"

Windows (PowerShell):

$env:GOOGLE_API_KEY="your_api_key_here"
4. Running the Application
Step 1: Populate Database

Run scraping scripts:

python "govt scholarships scrap.py"
python "web scrape.py"

Note: The Selenium script may take a few minutes due to dynamic page loading.

Step 2: Start Chatbot
python student_discounts_bot.py
Step 3: Interact

Example prompt:

Hi Student! Welcome to PerkPilotBot.
What are you looking for?
[1) Discounts  2) Government Scholarships/Schemes]
📌 Key Features
End-to-end pipeline: scraping → storage → AI querying
Context-aware chatbot powered by Gemini
Strict data grounding (no hallucinated responses)
Modular and extensible architecture
🚧 Potential Improvements
Replace SQLite with a scalable database (PostgreSQL / MongoDB)
Add semantic search instead of full prompt injection
Deploy as a web app (Flask / FastAPI)
Schedule automated scraping pipelines
Implement vector database (FAISS / Pinecone) for better retrieval

If you want, I can also:

Make this README resume-ready (short + impact focused)
Convert it into a GitHub portfolio highlight section
Add architecture diagram + flowchart for better presentation

Just tell me.

make it for github readme style 

Here is a clean, GitHub-ready README with proper formatting, badges, structure, and concise sections (optimized for recruiters and quick scanning):

🤖 PerkPilotBot

AI-powered CLI chatbot to discover student discounts and government scholarships using web scraping + Google Gemini

🚀 Features
🔍 Scrapes student discounts from multiple platforms
🎓 Extracts government scholarships from official portals
🤖 AI-powered chatbot (Google Gemini) for smart responses
💾 Local SQLite database for fast retrieval
⚡ Fully command-line based, lightweight, and modular
🧠 How It Works
1. Data Collection
Scrapes data using:
BeautifulSoup + requests → static websites
Selenium → dynamic content
Sources include:
Student discount platforms
Government scholarship portals
Stores cleaned data in SQLite:
discounts table
govt_scholarships table
2. AI Chatbot
Loads data from database
Prompts user for:
Discounts OR Scholarships
Injects relevant dataset into prompt
Uses Google Gemini (gemini-1.5-flash)
Ensures responses are strictly grounded in scraped data
🛠️ Tech Stack
Language: Python
AI: Google Gemini API (google-generativeai)
Web Scraping: Selenium, BeautifulSoup, Requests
Database: SQLite
📁 Project Structure
PerkPilotBot/
│── student_discounts_bot.py      # Main chatbot
│── web scrape.py                 # Discount scraper
│── govt scholarships scrap.py    # Scholarship scraper
│── student_discounts.db          # Database (generated)
│── print database contents.py    # Debug utility
│── websites.txt                  # Source references
│── README.md
⚙️ Setup
1. Clone Repo
git clone <your-repo-url>
cd PerkPilotBot
2. Install Dependencies
pip install google-generativeai requests beautifulsoup4 selenium
3. Set API Key
# Linux / macOS
export GOOGLE_API_KEY="your_api_key"

# Windows (CMD)
set GOOGLE_API_KEY="your_api_key"

# Windows (PowerShell)
$env:GOOGLE_API_KEY="your_api_key"
▶️ Usage
Step 1: Run Scrapers
python "govt scholarships scrap.py"
python "web scrape.py"
Step 2: Start Chatbot
python student_discounts_bot.py
Step 3: Example Interaction
Hi Student! Welcome to PerkPilotBot.
What are you looking for?
1) Discounts
2) Government Scholarships/Schemes
✨ Highlights
End-to-end pipeline: Scraping → Storage → AI Querying
Real-world use case for students
LLM grounded responses (no hallucination)
Clean modular structure
🚧 Future Improvements
🌐 Web app deployment (Flask / FastAPI)
🔎 Semantic search (FAISS / vector DB)
⏱️ Scheduled scraping automation
🗄️ Upgrade to PostgreSQL / MongoDB
📊 Add filtering & ranking system
