# PerkPilotBot

An intelligent AI-powered bot that helps students discover relevant discounts and government scholarships. PerkPilotBot combines web scraping, database management, and Google Gemini AI to provide personalized recommendations for student benefits.

## 🚀 How It Works

PerkPilotBot operates through a three-stage process:

### 1. Data Collection & Storage
- **Web Scraping**: Automated scrapers collect real-time data from popular student discount platforms
  - MyUNIDAYS (https://www.myunidays.com) - Student discount marketplace
  - Student Beans (https://www.studentbeans.com) - Global student discount platform
  - Government Scholarships (https://scholarships.gov.in) - Official Indian scholarship portal

- **Database Storage**: All scraped data is stored in a SQLite database (`student_discounts.db`) with two main tables:
  - `discounts`: Contains company offers, discount details, links, and expiry dates
  - `govt_scholarships`: Contains scholarship titles, details, application links, and deadlines

### 2. AI-Powered Intelligence
- **Google Gemini Integration**: Uses Gemini 1.5 Flash model for natural language processing
- **Contextual Understanding**: AI analyzes user queries against the database to find relevant matches
- **Personalized Responses**: Provides tailored recommendations with direct links to offers

### 3. User Interaction
- **Interactive CLI**: Simple command-line interface for user interaction
- **Smart Categorization**: Users can choose between discounts or scholarships
- **Instant Results**: Real-time AI-generated responses with actionable links

## 🏗️ System Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Web Scrapers  │ -> │  SQLite Database │ -> │   Gemini AI     │
│                 │    │                  │    │                 │
│ • MyUNIDAYS     │    │ • discounts      │    │ • Query         │
│ • Student Beans │    │ • govt_scholar-  │    │   Processing    │
│ • Scholarships  │    │   ships          │    │ • Response      │
│   .gov.in       │    │                  │    │   Generation    │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                 |                        |
                                 v                        v
                       ┌──────────────────┐    ┌─────────────────┐
                       │  Data Storage    │    │  User Interface │
                       │                  │    │                 │
                       │ • Company Info   │    │ • CLI Bot       │
                       │ • Discount %     │    │ • Query Input   │
                       │ • Links          │    │ • AI Response   │
                       │ • Expiry Dates   │    │ • Direct Links  │
                       └──────────────────┘    └─────────────────┘
```

## 📁 Project Structure

```
PerkPilotBot/
├── student_discounts_bot.py      # Main bot interface with Gemini AI
├── web scrape.py                 # Discount website scraper (MyUNIDAYS, Student Beans)
├── govt scholarships scrap.py    # Government scholarship scraper
├── print database contents.py    # Database viewer utility
├── student_discounts.db         # SQLite database (auto-generated)
├── websites.txt                 # List of target websites
└── README.md                    # This documentation
```

## 🛠️ Technical Implementation

### Data Scraping Pipeline
1. **MyUNIDAYS Scraper**: Uses `requests` and `BeautifulSoup` to extract discount data
2. **Student Beans Scraper**: Uses `Selenium` for dynamic content scraping with infinite scroll
3. **Government Scholarships**: Scrapes official scholarship portal for latest opportunities

### AI Integration
- **Model**: Google Gemini 1.5 Flash for fast, intelligent responses
- **Context**: AI receives entire database context for accurate matching
- **Filtering**: Smart filtering prevents promotion of specific platforms while providing relevant results

### Database Schema
```sql
-- Discounts Table
CREATE TABLE discounts (
    id INTEGER PRIMARY KEY,
    source TEXT,           -- Platform name (MyUNIDAYS, Student Beans)
    company TEXT,          -- Company offering discount
    link TEXT,             -- Direct link to offer
    discount TEXT,         -- Discount description
    expiry TEXT           -- Expiration date
);

-- Government Scholarships Table
CREATE TABLE govt_scholarships (
    id INTEGER PRIMARY KEY,
    title TEXT,            -- Scholarship name
    scheme_details TEXT,   -- Description
    link TEXT,             -- Application link
    expiry_dates TEXT     -- Application deadlines
);
```

## ⚙️ Setup & Installation

### Prerequisites
- Python 3.7+
- Google Gemini API Key
- Chrome WebDriver (for Selenium)

### Dependencies
```bash
# Install all dependencies at once
pip install -r requirements.txt

# Or install individually
pip install google-generativeai requests beautifulsoup4 selenium
```

### Environment Setup
1. Get a Google Gemini API key from [Google AI Studio](https://aistudio.google.com/)
2. Set the environment variable:
   ```bash
   export GOOGLE_API_KEY="your_api_key_here"
   ```

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/kumarharsh24/PerkPilotBot.git
   cd PerkPilotBot
   ```

2. Install Chrome WebDriver for Selenium

3. Run the scrapers to populate the database:
   ```bash
   python "web scrape.py"
   python "govt scholarships scrap.py"
   ```

4. Start the bot:
   ```bash
   python student_discounts_bot.py
   ```

## 🎯 Usage

1. **Start the Bot**: Run `python student_discounts_bot.py`
2. **Choose Category**: Select either "1) Discounts" or "2) Government Scholarships"
3. **Enter Query**: Describe what you're looking for (e.g., "laptop deals", "engineering scholarships")
4. **Get Results**: Receive AI-generated recommendations with direct links

### Example Interactions

**For Discounts:**
```
User: "What are you looking to buy?"
Input: "laptop for programming"
Output: AI-generated response with relevant laptop discounts and links
```

**For Scholarships:**
```
User: "What type of scholarships are you looking for?"
Input: "engineering undergraduate scholarships"
Output: AI-generated response with matching scholarship opportunities
```

## 🔧 Key Features

- **Real-time Data**: Fresh discount and scholarship information
- **AI-Powered Matching**: Intelligent query understanding and response generation
- **Direct Links**: Immediate access to offers and applications
- **Comprehensive Coverage**: Both commercial discounts and government scholarships
- **User-Friendly**: Simple CLI interface for easy interaction

## 🛡️ Privacy & Security

- **No Personal Data Storage**: Bot doesn't store user queries or personal information
- **API Key Security**: Requires secure handling of Google Gemini API key
- **Local Database**: All scraped data stored locally in SQLite

## 📊 Technologies Used

- **AI/ML**: Google Gemini API for natural language processing
- **Web Scraping**: Selenium, BeautifulSoup, Requests
- **Database**: SQLite for local data storage
- **Languages**: Python 3.x

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is open source. Please check the repository for license details.

## 🔍 Summary

**PerkPilotBot** is a comprehensive solution that bridges the gap between students and available benefits through intelligent automation:

1. **Automated Data Collection**: Continuously gathers fresh discount and scholarship data from multiple sources
2. **Intelligent Processing**: Uses Google Gemini AI to understand user queries and provide relevant recommendations  
3. **Direct Access**: Provides immediate links to offers and applications, saving time and effort
4. **Comprehensive Coverage**: Includes both commercial discounts and government scholarships in one place
5. **User-Friendly Interface**: Simple CLI that anyone can use without technical knowledge

**Perfect for students who want to**:
- Find relevant discounts before making purchases
- Discover scholarship opportunities they might have missed
- Get personalized recommendations instead of browsing endless lists
- Access up-to-date information with working links

The bot transforms scattered information across multiple websites into personalized, actionable recommendations through the power of AI.
