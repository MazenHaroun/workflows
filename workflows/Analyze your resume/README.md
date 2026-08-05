# Analyze Your Resume

An n8n workflow that scrapes matching LinkedIn jobs, analyzes them against your resume using an AI agent, and sends you a personalized 30-day career improvement plan on Telegram.

## How it works

1. **Input & Search Setup**
   - Downloads your resume (PDF) from Google Drive
   - Reads your target job criteria (keyword, location, experience level, remote, job type, Easy Apply) from Google Sheets
   - Builds a filtered LinkedIn job search URL
   - Scrapes the matching job links

2. **Process Job Postings**
   - Loops through each job link and scrapes the full job page
   - Extracts and cleans job attributes (description, job ID, apply link)
   - Aggregates all jobs into one batch

3. **Career Coach AI & Notification**
   - Runs the AI gap analysis against your resume
   - Sends the 30-day plan to Telegram

## Workflow overview

```
Schedule Trigger
  └─ Download file (Google Drive) → Extract from File (PDF)
  └─ Get row(s) in sheet (Google Sheets - job criteria)
       └─ Create search URL → Fetch Jobs from Linkedin → Extract Job Links
            └─ Limit → Loop Over Items → Wait → Fetch Job Page → Parse Job Attributes
                 └─ Aggregate Jobs → AI Agent (OpenAI) → Parse AI Output
                      └─ Send a text message (Telegram)
```

## Setup

1. Import `Analyze_your_resume.json` into n8n.
2. Configure credentials:
   - **Google Drive** – where your resume PDF is stored
   - **Google Sheets** – spreadsheet holding your target job criteria
   - **OpenAI** – chat model used by the AI Agent
   - **Telegram** – set your Chat ID in the "Send a text message" node (see the sticky note)
3. In Google Drive / Sheets nodes, select the correct file, spreadsheet, and sheet.
4. Activate the workflow.

> ⚠️ **Cost Safeguard**: The `Limit` node caps the payload sent to the AI. Do not bypass it, or large scrapes will cause high API token usage.
