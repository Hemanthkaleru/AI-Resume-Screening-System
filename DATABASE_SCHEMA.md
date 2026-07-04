# Database Schema Documentation

The system uses Airtable as the primary candidate database.

---

# Table: Candidates

Purpose:
Store candidate profiles, AI evaluation results, recruitment status, and interview information.

---

| Field Name            | Data Type     | Description                                                    |
| --------------------- | ------------- | -------------------------------------------------------------- |
| Candidate Name        | Text          | Full name of the candidate                                     |
| Email                 | Text (Unique) | Candidate email address                                        |
| Phone                 | Text          | Contact number                                                 |
| Location              | Text          | Candidate location                                             |
| Experience            | Number        | Total years of experience                                      |
| Education             | Text          | Education details                                              |
| Technical Skills      | Text          | Comma-separated technical skills                               |
| Match Score           | Number        | Final candidate score (0-100)                                  |
| Matching Skills       | Text          | Skills matching the job description                            |
| Missing Skills        | Text          | Required skills not present                                    |
| AI Summary            | Long Text     | AI-generated candidate summary                                 |
| Recommendation        | Single Select | Strong Fit, Possible Fit, Not a Fit                            |
| Application Status    | Single Select | New, Manual Review, Shortlisted, Interview Scheduled, Rejected |
| Email Subject         | Text          | Original email subject                                         |
| Sender Email          | Text          | Candidate email address                                        |
| Received At           | DateTime      | Resume submission timestamp                                    |
| Relevant Experience   | Long Text     | AI-generated experience summary                                |
| Resume Attachment     | Attachment    | Original uploaded resume                                       |
| Job Title Applied For | Text          | Target job role                                                |
| Interview Questions   | Long Text     | AI-generated interview questions                               |

---

# Recommendation Values

## Strong Fit

Candidate strongly matches the job requirements.

## Possible Fit

Candidate partially matches the requirements and requires manual review.

## Not a Fit

Candidate does not satisfy the required technical criteria.

---

# Application Status Flow

```text
New
 ↓
AI Evaluation
 ↓
 ├── Shortlisted
 │      ↓
 │ Interview Scheduled
 │
 ├── Manual Review
 │
 └── Rejected
```

---

# Data Relationships

Email Submission
↓
Resume File
↓
AI Parsing
↓
Candidate Record
↓
Matching Results
↓
Recruitment Actions

---

# Database Design Considerations

* Email field acts as the unique identifier.
* Resume files are stored in Google Drive and linked within Airtable.
* Status values support workflow automation routing.
* Long text fields store AI-generated insights and interview questions.
* Schema is extensible and can support additional recruitment stages.

---

# Scalability Considerations

The schema can be extended with additional fields:

* Resume Embeddings
* ATS Notes
* Interview Feedback
* Recruiter Comments
* Offer Status
* Joining Status
* Candidate Ranking
* Source Channel
* Hiring Pipeline Metrics

The current schema is normalized for small-to-medium recruitment workflows and can be migrated to relational databases such as PostgreSQL if required.
