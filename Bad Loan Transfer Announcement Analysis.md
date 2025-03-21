
## Project Overview

This project aims to scrape bad loan transfer announcements from the Banking Registration Center website, extract the data for analysis, and gain insights into China's non-performing loan market.

---

## 1. Data Collection

### 1.1 Web Crawler Setup
- Using Selenium for browser automation
- Configuring headless Chrome browser
- Setting user agents and browser options

```python
def setup_selenium():
    chrome_options = Options()
    chrome_options.add_argument("--headless")
    chrome_options.add_argument("--disable-gpu")
    # More configurations...
```

### 1.2 Announcement Scraping
- Target website: Banking Registration Center announcement page
- Keyword filtering: "Bad loans"
- Year filtering: 2024-2025
- Pagination handling: scraped 276 pages in total

```python
def crawl_announcements():
    # Get total page count
    total_pages = get_total_pages(driver)
    
    # Iterate through each page
    for i in range(1, total_pages + 1):
        # Get and parse announcements...
```

### 1.3 Data Storage
- Saving scraping results to CSV file: "BankingCenterAnnouncements.csv"
- Fields include: title, detail link, publication date

---

## 2. PDF File Processing

### 2.1 PDF Download
- Visiting announcement detail pages
- Extracting PDF links
- Downloading PDF files locally
- Normalizing file naming

```python
def download_file(url, dest_path):
    # File download logic...
```

### 2.2 PDF Merging
- Sorting downloaded PDF files by creation time
- Dividing into four groups for merging
- Generating four merged PDF files: merged1.pdf, merged2.pdf, merged3.pdf, merged4.pdf

```python
def merge_pdf_files():
    # PDF grouping and merging logic...
```

### 2.3 Content Extraction
- Using pdfplumber to extract from PDFs:
  - Plain text
  - Table data
  - Structured content (headings and paragraphs)

```python
def extract_pdf_and_save_csv(pdf_path, output_prefix="pdf"):
    # Extract PDF content and save to CSV...
```

### 2.4 Data Integration
- Merging all table data into a single CSV file: "merged_tables.csv"

---

## 3. Data Analysis

### 3.1 Excel Analysis
- Importing CSV files to Excel
- Data cleaning and preprocessing
- Statistical analysis and summarization

### 3.2 Key Statistics
- Total borrowers: 5,856,576 people
- Average age: 43.225 years
- Average overdue days: 1051.8175 days
- Asset count: 15,545,588 items
- Total unpaid principal and interest: 20.05 billion CNY

### 3.3 Key Findings
- **98% of non-performing assets have not been litigated**
- Average debt per person: 34,999.90 CNY
- Overdue loan borrowers mainly concentrated in the 41-45 age group, representing 6% of the total population

---

## 4. Data Visualization

### 4.1 Data Tables
- Creating summary tables showing key data from the four merged PDFs
- Calculating sums and averages

### 4.2 Derived Metrics
- Non-litigated/Asset ratio: 98%
- Average debt per person: 34,999.90 CNY
- Age distribution compared to population demographics

---

## 5. Conclusions and Findings

### 5.1 Main Conclusions
- The vast majority of bad loans (98%) have not entered litigation proceedings
- The average age of bad loan borrowers is 43 years, mainly concentrated in the 41-45 age group
- Average overdue time exceeds 1,000 days (approximately 3 years)
- Average debt amount is approximately 35,000 CNY per case

### 5.2 Business Implications
- Financial institutions may prefer non-litigation approaches for bad loan disposal
- Middle-aged population groups are high-risk groups for bad loans
- Long overdue periods indicate difficulty in recovery

---

## 6. Technical Implementation

The complete project implementation via Python script includes these main steps:

1. Installing necessary dependencies
2. Scraping Banking Registration Center announcements
3. Downloading PDF files from announcements
4. Merging PDF files
5. Extracting content from PDFs to CSV
6. Using Excel for data analysis and visualization

```python
def main():
    # Step 1: Ensure required dependencies are installed
    print("🔍 Step 1: Ensuring required dependencies are installed...")
    
    # Step 2: Scrape Banking Registration Center announcements
    print("\n🔍 Step 2: Scraping Banking Registration Center announcements...")
    csv_file = crawl_announcements()
    
    # More steps...
```
