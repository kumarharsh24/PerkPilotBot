# PerkPilotBot - Quick Start Guide

## Overview
PerkPilotBot is an AI-powered assistant that helps students find discounts and scholarships by combining web scraping, database storage, and Google Gemini AI.

## Quick Setup (5 minutes)

### 1. Prerequisites
- Python 3.7+ installed
- Google Gemini API Key ([Get one here](https://aistudio.google.com/))
- Chrome browser (for web scraping)

### 2. Installation
```bash
# Clone repository
git clone https://github.com/kumarharsh24/PerkPilotBot.git
cd PerkPilotBot

# Install required packages
pip install google-generativeai requests beautifulsoup4 selenium
```

### 3. Environment Setup
```bash
# Set your Google Gemini API key
export GOOGLE_API_KEY="your_api_key_here"

# On Windows:
set GOOGLE_API_KEY=your_api_key_here
```

### 4. Start Using
```bash
# Run the bot (database already contains sample data)
python student_discounts_bot.py
```

## Usage Examples

### Example 1: Finding Laptop Discounts
```
Hi Student! Welcome to PerkPilotBot. What are you looking for [1) Discounts 2) Government Scholarships]? 1
What are you looking to buy? laptop for college

Response: "Hi! I'm PerkPilotBot, and I'd be happy to help you find laptop deals for college! 
Based on current offers, here are some great options:

🖥️ **Dell** - Student discounts available with verification
🍎 **Apple** - Education pricing for MacBooks  
💻 **HP** - Special student rates on laptops
⚡ **Best Buy** - Student discount program

Visit the websites directly through the provided links for the latest deals and verification requirements."
```

### Example 2: Finding Engineering Scholarships
```
Hi Student! Welcome to PerkPilotBot. What are you looking for [1) Discounts 2) Government Scholarships]? 2
What type of scholarships are you looking for? engineering scholarships for undergraduate students

Response: "Hello! I'm PerkPilotBot, here to help you find engineering scholarships! 
Based on current government schemes:

🎓 **National Scholarship Portal** offers several engineering scholarships:
- Merit-based scholarships for technical education
- State-specific engineering student support schemes  
- Central sector scholarship schemes for technical students

Visit https://scholarships.gov.in for detailed eligibility criteria and application procedures. 
Make sure to check application deadlines as they vary by scheme."
```

## How the System Works (Simple Overview)

```
1. WEB SCRAPERS → 2. DATABASE → 3. AI BOT → 4. USER
   Collect fresh      Store         Smart          Get personalized
   discount &         organized     responses      recommendations
   scholarship        data          with context   with direct links
   data
```

### Step-by-Step Process:
1. **Data Collection**: Scrapers automatically gather discounts from MyUNIDAYS, Student Beans, and scholarships from scholarships.gov.in
2. **Smart Storage**: All data organized in SQLite database with company info, links, discounts, and expiry dates
3. **AI Processing**: When you ask a question, Gemini AI analyzes your query against the entire database
4. **Personalized Results**: You get relevant recommendations with direct links to apply or claim offers

## Update Data (Optional)

To refresh with latest discounts and scholarships:

```bash
# Update discount data (takes 2-3 minutes)
python "web scrape.py"

# Update scholarship data (takes 1 minute)  
python "govt scholarships scrap.py"
```

## View Database Contents

To see what data is available:

```bash
python "print database contents.py"
```

## Troubleshooting

**"API key not found" error:**
- Make sure you set the GOOGLE_API_KEY environment variable
- Restart your terminal after setting the variable

**Selenium/Chrome driver errors:**
- Make sure Chrome browser is installed
- Download ChromeDriver and add to PATH if needed

**Empty responses:**
- Database might be empty - run the scraper scripts first
- Check your internet connection

**No relevant results:**
- Try broader search terms
- The AI will tell you if no matching offers are found

## Project Structure
```
PerkPilotBot/
├── student_discounts_bot.py      # 🤖 Main bot (start here)
├── web scrape.py                 # 🕷️ Discount scraper  
├── govt scholarships scrap.py    # 🎓 Scholarship scraper
├── student_discounts.db         # 💾 Data storage
└── README.md                    # 📖 Full documentation
```

## Need Help?

- **Full Documentation**: See README.md for complete technical details
- **Technical Details**: See TECHNICAL_DOCUMENTATION.md for developer information
- **Issues**: Check the repository's issue tracker for common problems

**Tip**: The bot works best with specific queries like "textbooks", "software discounts", "STEM scholarships" rather than very general terms.