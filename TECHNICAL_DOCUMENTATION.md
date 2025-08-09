# PerkPilotBot - Technical Documentation

## Detailed System Analysis

### Component Breakdown

#### 1. Main Bot Interface (`student_discounts_bot.py`)

**Purpose**: Primary user interface that leverages Google Gemini AI for intelligent responses.

**Key Functions**:
- Establishes connection to Google Gemini API using environment variable `GOOGLE_API_KEY`
- Connects to SQLite database to retrieve current offers and scholarships
- Provides interactive CLI for user input
- Generates contextualized AI responses based on user queries

**Technical Implementation**:
```python
# API Configuration
genai.configure(api_key=api_key)
model = genai.GenerativeModel("gemini-1.5-flash")

# Database Query
cursor.execute('SELECT * FROM discounts')
cursor.execute('SELECT * FROM govt_scholarships')

# AI Response Generation
response = model.generate_content(f"context: {database_data}, query: {user_input}")
```

**Data Flow**:
1. User selects category (discounts/scholarships)
2. System retrieves relevant database records
3. User enters specific query
4. AI processes query with database context
5. Formatted response with links provided to user

#### 2. Discount Scraper (`web scrape.py`)

**Purpose**: Automated data collection from student discount platforms.

**Target Websites**:
- **MyUNIDAYS**: Static content scraping using `requests` + `BeautifulSoup`
- **Student Beans**: Dynamic content scraping using `Selenium` WebDriver

**Technical Approach**:

**MyUNIDAYS Scraping**:
```python
# Static scraping approach
response = requests.get("https://www.myunidays.com/IN/en-IN/list/all/AtoZ")
soup = BeautifulSoup(response.content, 'html.parser')
articles = soup.find_all('article', class_='tile')
```

**Student Beans Scraping**:
```python
# Dynamic scraping with infinite scroll
driver = webdriver.Chrome()
driver.get("https://www.studentbeans.com/student-discount/us/all")

# Infinite scroll implementation
while True:
    driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
    time.sleep(scroll_pause)
    new_height = driver.execute_script("return document.body.scrollHeight")
    if new_height == last_height:
        break
```

**Data Extraction Pattern**:
- Company name identification
- Discount percentage/description parsing
- Link extraction and URL formatting
- Expiry date detection
- Database insertion with error handling

#### 3. Scholarship Scraper (`govt scholarships scrap.py`)

**Purpose**: Collects government scholarship information from official Indian portal.

**Target**: https://scholarships.gov.in/All-Scholarships

**Technical Implementation**:
```python
# Government portal scraping
url = "https://scholarships.gov.in/All-Scholarships"
soup = BeautifulSoup(response.content, 'html.parser')
scholarship_blocks = soup.find_all('div', class_='row mb-4 border-1 border-bottom')
```

**Data Points Extracted**:
- Scholarship title
- Scheme details
- Application links
- Expiry dates
- Eligibility criteria (embedded in details)

#### 4. Database Utility (`print database contents.py`)

**Purpose**: Development tool for database inspection and debugging.

**Functionality**:
- Connects to SQLite database
- Retrieves and displays all records
- Formatted output for easy reading
- Helps verify scraping success

### Database Design

#### Schema Analysis

**Discounts Table**:
```sql
CREATE TABLE discounts (
    id INTEGER PRIMARY KEY,
    source TEXT,        -- Platform identifier
    company TEXT,       -- Brand/company name
    link TEXT,          -- Direct offer URL
    discount TEXT,      -- Offer description
    expiry TEXT        -- Expiration information
);
```

**Government Scholarships Table**:
```sql
CREATE TABLE govt_scholarships (
    id INTEGER PRIMARY KEY,
    title TEXT,            -- Official scholarship name
    scheme_details TEXT,   -- Description/summary
    link TEXT,             -- Application portal link
    expiry_dates TEXT     -- Deadline information
);
```

#### Data Relationships
- No foreign key relationships (denormalized for simplicity)
- Each table operates independently
- Data integrity maintained through application logic

### AI Integration Details

#### Gemini API Usage
- **Model**: `gemini-1.5-flash` for optimal speed/quality balance
- **Context Window**: Entire database content passed as context
- **Prompt Engineering**: Structured prompts with specific instructions

#### Prompt Structure
```python
# Discount queries
f"these are the current offers {rows}, from these answer this prompt and remember that your name is PerkPilotBot and dont mention MyUnidays or StudentBeans and also give link to the website (logo column contains the link) if you cant find an appropriate website based on the offers list i gave, then just say that there are no currently offers {user_query}"

# Scholarship queries  
f"these are the current scholarships {rows2}, from these answer this prompt and remember that your name is PerkPilotBot also give link to the website if you cant find an appropriate website based on the scholarships list i gave, then just say that there are no currently scholarships dont say anything more {user_query}"
```

#### Response Processing
- AI returns natural language responses
- Includes relevant links when available
- Filters out platform-specific branding
- Provides fallback messages for no matches

### Error Handling & Robustness

#### Web Scraping Resilience
- Try-catch blocks for element extraction
- Graceful handling of missing data
- Timeout management for Selenium
- HTTP status code validation

#### Database Operations
- Automatic table creation if not exists
- Proper connection management
- Transaction handling with commit/rollback
- SQL injection prevention through parameterized queries

#### API Integration
- Environment variable validation for API key
- Graceful degradation on API failures
- Rate limiting considerations

### Performance Considerations

#### Scraping Optimization
- Selenium scroll optimization for Student Beans
- Request batching for multiple pages
- Sleep intervals to avoid rate limiting
- Chrome driver configuration for headless operation

#### Database Performance
- SQLite for lightweight, local storage
- Indexed primary keys for fast retrieval
- Minimal data types for storage efficiency

#### AI Response Time
- Gemini 1.5 Flash for fastest model variant
- Context optimization to stay within token limits
- Single-shot inference without conversation history

### Security Considerations

#### API Key Management
- Environment variable requirement
- No hardcoded credentials
- Proper key validation before usage

#### Web Scraping Ethics
- Respectful scraping with delays
- Robots.txt compliance consideration
- No aggressive scraping patterns

#### Data Privacy
- No personal user data storage
- Local database only
- No query logging or tracking

### Maintenance & Updates

#### Data Freshness
- Manual scraper execution required
- No automated scheduling implemented
- Database overwrite on each scraping run

#### Scalability Limitations
- Single-threaded scraping
- Local SQLite storage
- No distributed processing

#### Future Enhancement Opportunities
- Automated scheduling (cron jobs)
- Additional discount platforms
- Database optimization
- Web interface development
- User authentication system
- Personalized recommendations

### Troubleshooting Guide

#### Common Issues
1. **API Key Errors**: Verify `GOOGLE_API_KEY` environment variable
2. **Selenium Failures**: Ensure Chrome WebDriver is installed and accessible
3. **Database Errors**: Check file permissions for SQLite database
4. **Scraping Failures**: Verify target website structure hasn't changed
5. **Empty Responses**: Run scrapers to populate database before using bot

#### Debug Tools
- Use `print database contents.py` to verify data
- Check console output for scraping errors  
- Validate API responses manually
- Test individual components separately

This technical documentation provides developers with detailed understanding of PerkPilotBot's architecture, implementation details, and operational considerations.