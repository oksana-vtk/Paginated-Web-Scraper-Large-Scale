# Large-scale Paginated Scraper 

This project is a robust Selenium-based web scraper designed to extract 
5K+ pages of agent data (10 agents per page) from a paginated web directory. 
It supports large-scale data collection with features like automatic backup, agent indexing, 
and headless browser execution.

## Features

- Scrapes agent info: **name, years of service, badges, languages, phone, email, website**
- Can pause and resume scraping using page ranges, with automatic backup saving
- Handles stale DOM references with retry logic
- Saves both final and incremental backup CSV files
- Automatically restarts browser to manage memory
- Detailed logging for each state (to file and console)
- Environment-based configuration via `.env` file

## Requirements

- Python 3.9+
- pandas
- selenium
- python-dotenv
- Google Chrome
- ChromeDriver (compatible with your Chrome version)

## Environment Setup

Create a .env file:

- URL_1=https://example.com/state1?page={page}
- URL_2=https://example.com/state2?page={page}
- STATE_1=state_1
- STATE_2=state_2
- OUTPUT_FILE_1=agents_state_1.csv
- OUTPUT_FILE_2=agents_state_2.csv
- BACKUP_FILE_1=agents_backup_state_1.csv
- BACKUP_FILE_2=agents_backup_state_2.csv

## Usage

Run the scraper for a specific state and page range or run in chunks for large-scale scraping:

**agents_from_state(URL_1, STATE_1, OUTPUT_FILE_1, BACKUP_FILE_1, start_page, finish_page)**

## Result table includes:

    Column	            Description
    Page	            Source pagination page
    Agent_index         Unique index (e.g., agent_123)
    Name	            Full agent name
    Years of Service    Experience listed
    Badges	            Any visible certification tags
    Phone	            Contact phone
    Email	            Email address
    Website	            Agent's website (if available)
    Languages           Languages spoken (if listed)
    State	            Scraped state

## Total Scraped 
- state_1: 5K+ pages, 50K+ agents
- state_2: 4.6K+ pages, 46K+ agents

## Files Generated
- `agents_state_1.csv` - full final output, total 50K+ rows
- `agents_state_2.csv` - full final output, total 46+K
- `agents_backup_state_1.csv` - rolling backup every 100 agents
- `agents_backup_state_2.csv` - rolling backup every 100 agents
- `state_1_log_info.log`
- `state_2_log_info.log`

## Notes

- Backup file only saves newly scraped records to avoid duplication.
- Logger is automatically created per state
- Random delays and retry logic are implemented to reduce the chance of blocking or errors.

