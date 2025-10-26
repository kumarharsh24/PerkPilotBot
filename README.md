```markdown
# PerkPilotBot 🤖

PerkPilotBot is a command-line chatbot built with the Google Gemini API. It helps students find relevant discounts and government scholarships by scraping various web sources and storing the information in a local SQLite database.

## 🚀 How It Works

The project operates in two main phases:

1.  **Data Collection (Scraping):**
    * Python scripts use `BeautifulSoup` and `Selenium` to scrape data from multiple websites.
    * `web scrape.py` gathers student discounts from **MyUNIDAYS** (using `requests` and `BeautifulSoup`) and **Student Beans** (using `Selenium` for dynamic content).
    * `govt scholarships scrap.py` gathers scholarship information from India's **National Scholarship Portal** (`scholarships.gov.in`).
    * All collected data is cleaned and stored in a local SQLite database (`student_discounts.db`) in two separate tables: `discounts` and `govt_scholarships`.

2.  **Chatbot Interaction (AI):**
    * The main `student_discounts_bot.py` script runs the chatbot.
    * It first loads all discount and scholarship data from the `student_discounts.db` database.
    * It asks the user if they are looking for **Discounts** or **Scholarships**.
    * Based on the user's query, it dynamically creates a large prompt for the **Google Gemini API** ("gemini-1.5-flash"). This prompt includes the *entire set* of relevant data (either all discounts or all scholarships) and instructs the AI to answer *only* using that data.
    * The bot then prints the AI's generated, helpful response.

## 🛠️ Technologies Used

* **AI:** Google Gemini API (`google-generativeai`)
* **Web Scraping:** Selenium, BeautifulSoup4, Requests
* **Database:** SQLite3
* **Language:** Python

## 📁 File Structure

```

.
├── student\_discounts\_bot.py  \# The main chatbot script that interacts with the user and Gemini API.
├── web scrape.py             \# Script to scrape student discounts from MyUNIDAYS and Student Beans.
├── govt scholarships scrap.py  \# Script to scrape scholarships from scholarships.gov.in.
├── student\_discounts.db      \# SQLite database where all scraped data is stored.
├── print database contents.py  \# A helper script to print database contents (for debugging).
├── websites.txt              \# A reference file containing the source URLs.
└── README.md                 \# This file.

````

## ⚙️ Setup and Usage

Follow these steps to run the project locally.

### 1. Prerequisites

* Python 3.x
* Google Chrome (for Selenium)
* Chrome WebDriver (must match your Chrome version)

### 2. Installation

1.  **Clone the repository:**
    ```bash
    git clone <your-repo-url>
    cd PerkPilotBot
    ```

2.  **Create a `requirements.txt` file** with the following content:
    ```
    google-generativeai
    requests
    beautifulsoup4
    selenium
    ```

3.  **Install the dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

### 3. Set Up Google API Key

You must set your Google API key as an environment variable.

**On macOS/Linux:**
```bash
export GOOGLE_API_KEY="your_api_key_here"
````

**On Windows (Command Prompt):**

```bash
set GOOGLE_API_KEY="your_api_key_here"
```

**On Windows (PowerShell):**

```bash
$env:GOOGLE_API_KEY="your_api_key_here"
```

### 4\. Running the Project

1.  **Populate the Database:**
    You must run the scraping scripts first to create and fill the `student_discounts.db` file.

    ```bash
    python "govt scholarships scrap.py"
    python "web scrape.py"
    ```

    *Note: The `web scrape.py` script using Selenium may take a few minutes to run as it scrolls to load all data.*

2.  **Run the Chatbot:**
    Once the database is populated, you can start the bot.

    ```bash
    python student_discounts_bot.py
    ```

3.  **Interact with the Bot:**
    The bot will greet you and ask what you're looking for.

    ```
    Hi Student! Welcome to PerkPilotBot. What are you looking for [1) Discounts 2) Government Scholarships/Schemes]?
    ```

<!-- end list -->

```
```
