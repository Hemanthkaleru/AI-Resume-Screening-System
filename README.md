# AI-Powered Resume Screening & Recruitment Automation System

## Overview

This project is an end-to-end AI-powered recruitment automation workflow built using **n8n**, **Groq LLM APIs**, **Airtable**, **Google Drive**, **Gmail**, and **Google Calendar**.

The system automatically processes resumes received via email, extracts candidate information using AI, evaluates candidates against predefined job descriptions, stores results in Airtable, and automates interview scheduling and recruiter notifications.

The goal of this project is to reduce manual resume screening effort and accelerate recruitment workflows through intelligent automation.

---

# Features

### Automated Resume Intake

* Monitors recruitment inbox for new emails with attachments
* Downloads resume attachments automatically
* Marks processed emails as read

### Multi-Format Resume Processing

Supports:

* PDF resumes
* DOCX resumes

Unsupported files are automatically ignored.

---

# Resume Parsing using AI

Uses Groq LLM to extract structured candidate information:

* Candidate Name
* Email Address
* Phone Number
* Location
* Total Experience
* Current Role
* Current Company
* Education
* Technical Skills
* Soft Skills
* Certifications
* Languages
* Projects
* LinkedIn Profile

---

# AI-Based Candidate Evaluation

The workflow compares candidate profiles against predefined job descriptions and generates:

* Match Score (0–100)
* Matching Skills
* Missing Skills
* Relevant Experience Summary
* Potential Concerns
* AI Summary
* Hiring Recommendation

Recommendations:

* Strong Fit
* Possible Fit
* Not a Fit

---

# Deterministic Scoring Engine

To ensure reproducible results, candidate scoring is performed using rule-based evaluation on critical skill categories:

| Category                  | Weight |
| ------------------------- | ------ |
| Python                    | 25     |
| Frameworks (Django/Flask) | 25     |
| Databases                 | 15     |
| Testing                   | 15     |
| Git/GitHub                | 10     |
| Docker                    | 10     |

Total Score = 100

Application Status Rules:

* Match Score ≥ 80 → Shortlisted
* Match Score 60–79 → Manual Review
* Match Score < 60 → Rejected

---

# Automated Actions

## Shortlisted Candidates

* Generate AI interview questions
* Send interview invitation email
* Create Google Calendar event
* Update Airtable status to Interview Scheduled

## Manual Review Candidates

* Send recruiter notification email
* Store candidate for manual review

## Rejected Candidates

* Store candidate information
* No further action required

---

# Technology Stack

## Workflow Automation

* n8n

## AI Services

* Groq API
* Llama-3.1-8b-instant

## Database

* Airtable

## Storage

* Google Drive

## Communication

* Gmail API
* Google Calendar API

## Programming

* JavaScript
* JSON

---

# Solution Architecture

Email Inbox
↓
Gmail Trigger
↓
Resume Download
↓
PDF/DOCX Extraction
↓
Groq Resume Parser
↓
JSON Validation & Cleaning
↓
Job Description Matching
↓
Deterministic Scoring Engine
↓
Candidate Record Creation
↓
Airtable Database
↓
Decision Engine
├── Shortlisted
├── Manual Review
└── Rejected
↓
Interview Questions
↓
Email Notifications
↓
Google Calendar Scheduling

---

# Project Structure

```
AI-Resume-Screening-System
│
├── workflow/
│   └── My workflow.json
│
├── samples/
│   ├── ArjunMehta(ST).pdf
│   ├── SnehaRao(M).pdf
│   └── RameshIyer(W).pdf
│
├── README.md
├── PROMPTS.md
├── DATABASE_SCHEMA.md
└── TEST_CASES.md
```

---

# Setup Instructions

## Prerequisites

* n8n
* Groq API Key
* Gmail OAuth Credentials
* Google Drive OAuth Credentials
* Google Calendar OAuth Credentials
* Airtable Personal Access Token

---

# Installation

## Clone Repository

```bash
git clone <repository-url>
cd AI-Resume-Screening-System
```

## Start n8n

```bash
docker run -it --rm \
-p 5678:5678 \
-v ~/.n8n:/home/node/.n8n \
docker.n8n.io/n8nio/n8n
```

Open:

http://localhost:5678

---

# Import Workflow

1. Open n8n
2. Click Import Workflow
3. Select:

```
workflow/My workflow.json
```

4. Configure credentials:

   * Groq API
   * Gmail OAuth
   * Google Drive OAuth
   * Google Calendar OAuth
   * Airtable API

5. Activate workflow.

---

# Environment Variables

Example:

```env
GROQ_API_KEY=your_groq_api_key
AIRTABLE_TOKEN=your_airtable_token
GOOGLE_CLIENT_ID=your_client_id
GOOGLE_CLIENT_SECRET=your_client_secret
```

---

# Database Schema

## Candidates Table

| Field                 | Type          |
| --------------------- | ------------- |
| Candidate Name        | Text          |
| Email                 | Text          |
| Phone                 | Text          |
| Location              | Text          |
| Experience            | Number        |
| Education             | Text          |
| Technical Skills      | Text          |
| Match Score           | Number        |
| Matching Skills       | Text          |
| Missing Skills        | Text          |
| AI Summary            | Long Text     |
| Recommendation        | Single Select |
| Application Status    | Single Select |
| Email Subject         | Text          |
| Sender Email          | Text          |
| Received At           | DateTime      |
| Relevant Experience   | Long Text     |
| Resume Attachment     | Attachment    |
| Job Title Applied For | Text          |
| Interview Questions   | Long Text     |

---

# Sample Test Data

## Test Case 1

Resume:
ArjunMehta(ST).pdf

Expected Result:

* Strong Fit
* Match Score > 80
* Shortlisted
* Interview Scheduled

---

## Test Case 2

Resume:
SnehaRao(M).pdf

Expected Result:

* Possible Fit
* Manual Review

---

## Test Case 3

Resume:
RameshIyer(W).pdf

Expected Result:

* Not a Fit
* Rejected

---

# Error Handling

The workflow includes:

* Retry mechanism for external API calls
* JSON validation and cleanup
* Fallback extraction methods
* Centralized error trigger
* Graceful handling of unsupported files
* Manual review routing for uncertain candidates

---

# Scalability Considerations

* Modular workflow design
* Stateless AI processing
* Airtable as centralized candidate repository
* Separate parsing and matching stages
* Retry policies for transient failures
* Support for multiple job descriptions
* Easy integration with additional ATS platforms

---

# Security Considerations

* API keys stored as n8n credentials and environment variables.
* Unsupported files are automatically ignored.
* Only PDF and DOCX resumes are processed.
* Candidate data is stored in controlled systems (Airtable and Google Drive).
* Workflow retries and centralized error handling prevent incomplete executions.
* OAuth authentication is used for Google services.
* Secrets are never hardcoded inside workflow nodes.

---

# Future Improvements

* Multi-resume batch processing
* Resume ranking dashboard
* Advanced semantic search using vector databases
* Human feedback loop for continuous model improvement
* Integration with LinkedIn and ATS platforms
* Analytics dashboard and recruitment metrics
* Support for additional file formats

---

# Demo

The demo video demonstrates:

1. Workflow import and setup
2. Resume submission through email
3. AI-based resume extraction
4. Candidate evaluation and scoring
5. Airtable record creation
6. Interview email generation
7. Google Calendar scheduling
8. Error handling scenarios

---

# Author

Hemanth Kaleru

Software Engineer | Python Backend Developer | Generative AI Engineer
