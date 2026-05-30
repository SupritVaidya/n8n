# AI-Powered Job Search Automation

An automated job search pipeline built with n8n that scrapes 
LinkedIn daily, uses GPT-4o-mini to score job matches against 
a candidate resume, filters high-quality matches, generates 
detailed fit justifications, and saves results to Google Sheets 
and Google Docs — fully automated with zero manual effort.

## How it works

1. **Scheduled Trigger** — runs daily at 16:30
2. **Resume Fetch** — downloads the candidate's latest PDF 
   resume from Google Drive
3. **LinkedIn Scraper** — scrapes up to 100 .NET/C# 
   Werkstudent job postings from LinkedIn via Apify API
4. **Keyword Filter** — custom JavaScript filters results to 
   working-student roles only (Werkstudent, Teilzeit, 
   Student Assistant etc.)
5. **Job Match AI Agent** — GPT-4o-mini scores each job 
   against the resume from 0-100 using structured output
6. **Quality Gate** — only jobs scoring 75+ proceed further
7. **Fit Justification Agent** — generates a 200-250 word 
   professional fit analysis for each qualifying job mapping 
   resume evidence to job requirements
8. **Output** — qualifying jobs saved to Google Sheets tracker 
   and individual fit reports created in Google Docs

## Pipeline Architecture
Schedule Trigger
→ Fetch Resume (Google Drive)
→ Extract PDF Text
→ Scrape LinkedIn Jobs (Apify)
→ Merge Resume + Jobs
→ Keyword Filter (JavaScript)
→ Batch Processing (3 at a time)
→ Job Match AI Agent (GPT-4o-mini)
→ Quality Gate (score ≥ 75)
→ Google Sheets (job tracker)
→ Google Docs (fit report per company)
→ Fit Justification Agent (GPT-4o-mini)

## Tech Stack

- **n8n** — workflow orchestration
- **OpenAI GPT-4o-mini** — job match scoring and fit analysis
- **Apify** — LinkedIn job scraping
- **Google Drive** — resume storage
- **Google Sheets** — job tracking dashboard
- **Google Docs** — per-company fit reports
- **JavaScript** — custom keyword filtering logic

## Key Features

- Fully automated — runs daily without manual input
- Resume-aware scoring — AI reads actual resume content, 
  not just keywords
- Structured output parsing — enforces consistent JSON 
  schema from AI responses
- Batch processing — handles rate limits gracefully
- Quality filtering — eliminates irrelevant postings before 
  AI processing to reduce API costs