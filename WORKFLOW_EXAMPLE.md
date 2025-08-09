# PerkPilotBot - Complete Workflow Example

## Full System Demonstration

This example shows how all components of PerkPilotBot work together to help a student find laptop discounts.

### Step 1: Data Collection (Backend Process)

```bash
# Run web scraper to collect fresh discount data
python "web scrape.py"
```

**What happens internally:**
1. **MyUNIDAYS Scraper** visits https://www.myunidays.com/IN/en-IN/list/all/AtoZ
   - Extracts company names, discount percentages, and links
   - Example data collected: "Dell - 10% student discount"

2. **Student Beans Scraper** visits https://www.studentbeans.com/student-discount/us/all  
   - Uses Selenium to handle dynamic content
   - Scrolls through infinite scroll to load all offers
   - Example data: "Apple - Education pricing on MacBooks"

3. **Database Storage**
   ```sql
   INSERT INTO discounts VALUES (
       1, 'MyUNIDAYS', 'Dell', 'https://www.myunidays.com/dell-link', 
       '10% off laptops', '2024-12-31'
   );
   ```

### Step 2: Scholarship Data (Parallel Process)

```bash
# Run scholarship scraper  
python "govt scholarships scrap.py"
```

**Government portal scraping:**
- Visits https://scholarships.gov.in/All-Scholarships
- Extracts scholarship names, deadlines, and application links
- Stores in `govt_scholarships` table

### Step 3: User Interaction (Frontend)

```bash
# Student starts the bot
python student_discounts_bot.py
```

**Interactive session:**
```
Hi Student! Welcome to PerkPilotBot. What are you looking for [1) Discounts 2) Government Scholarships]? 1
What are you looking to buy? laptop for computer science studies
```

### Step 4: AI Processing (Behind the Scenes)

**System workflow:**
1. **Database Query**: Retrieves all 139 discount records
2. **Context Preparation**: Formats data for AI consumption
3. **Prompt Construction**:
   ```python
   prompt = f"these are the current offers {database_rows}, from these answer this prompt and remember that your name is PerkPilotBot and dont mention MyUnidays or StudentBeans and also give link to the website if you cant find an appropriate website based on the offers list i gave, then just say that there are no currently offers laptop for computer science studies"
   ```
4. **Gemini AI Call**: Sends prompt to Google Gemini 1.5 Flash model
5. **Response Generation**: AI analyzes query against database and generates relevant response

### Step 5: Intelligent Response

**AI Output:**
```
Hi! I'm PerkPilotBot, here to help you find laptop deals for your computer science studies! 

Based on current offers, here are some excellent options:

🖥️ **Dell** - Great student discounts on laptops perfect for programming
   Link: https://www.myunidays.com/dell-student-discount

💻 **HP** - Student pricing on powerful laptops suitable for coding
   Link: https://www.studentbeans.com/hp-education-store

🍎 **Apple** - Education pricing on MacBooks, popular among CS students  
   Link: https://www.apple.com/education-store

⚡ **Lenovo** - Student discounts on ThinkPads, excellent for development
   Link: https://www.lenovo.com/student-discount

💡 **Microsoft** - Student pricing on Surface laptops with development tools
   Link: https://www.microsoft.com/education-store

Visit these links to verify your student status and claim your discounts. Most require a .edu email address or student verification through services like SheerID.

Happy coding! 🎓💻
```

## Technical Flow Diagram

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│  Web Scrapers   │    │  SQLite Database │    │   User Query    │
│                 │    │                  │    │                 │
│ MyUNIDAYS ────┐ │    │ ┌─────────────┐  │    │ "laptop for CS  │
│ Student Beans ├─┼────┼─┤ discounts   │  │    │  studies"       │
│ Scholarships  │ │    │ │ (139 rows)  │  │    │                 │
└─────────────────┘    │ └─────────────┘  │    └─────────────────┘
                       │                  │             │
                       │ ┌─────────────┐  │             │
                       │ │govt_scholar-│  │             │
                       │ │ships(27rows)│  │             │
                       │ └─────────────┘  │             │
                       └──────────────────┘             │
                                │                       │
                                ▼                       ▼
                       ┌──────────────────┐    ┌─────────────────┐
                       │  Context Data    │    │  Gemini AI      │
                       │                  │    │                 │
                       │ All discount +   │────┤ • Query Analysis│
                       │ scholarship data │    │ • Context Match │
                       │ sent to AI       │    │ • Response Gen  │
                       └──────────────────┘    └─────────────────┘
                                                        │
                                                        ▼
                                               ┌─────────────────┐
                                               │ Smart Response  │
                                               │                 │
                                               │ • Relevant links│
                                               │ • No platform   │
                                               │   branding      │
                                               │ • Helpful tips  │
                                               └─────────────────┘
```

## Real Database Sample

**Actual discount record in database:**
```sql
SELECT * FROM discounts WHERE company LIKE '%Dell%' LIMIT 1;

Result:
ID: 23
Source: MyUNIDAYS  
Company: Dell
Link: https://www.myunidays.com/IN/en-IN/view/online/dell-in
Discount: Up to 10% off
Expiry: N/A
```

**How AI uses this data:**
- Recognizes "Dell" matches "laptop" query
- Formats response without mentioning "MyUNIDAYS" (as per instructions)
- Includes the actual link from database
- Adds contextual information about student verification

## Key Benefits Demonstrated

1. **Data Freshness**: Scraped data ensures current offers
2. **AI Intelligence**: Natural language understanding of user intent  
3. **Direct Access**: Working links provided immediately
4. **No Manual Searching**: One query replaces visiting multiple websites
5. **Personalized Results**: CS-specific laptop recommendations
6. **Time Saving**: Instant results vs. hours of manual research

## Error Handling Examples

**Scenario 1: No matches found**
```
Query: "rocket ship discount"
Response: "I'm sorry, but there are no current offers for rocket ships in our database."
```

**Scenario 2: API issues**
```
Error: "API key not found. Make sure to set the GOOGLE_API_KEY environment variable."
Solution: Set the environment variable and restart
```

**Scenario 3: Database empty**
```
Response: "No current offers available"
Solution: Run web scrapers to populate database
```

This complete workflow shows how PerkPilotBot transforms raw web data into intelligent, personalized recommendations for students.