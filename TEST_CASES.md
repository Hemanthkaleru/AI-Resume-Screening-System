# Test Cases Documentation

This document describes the functional testing performed on the AI Resume Screening & Recruitment Automation System.

---

# Test Environment

Workflow Engine:
n8n

LLM Provider:
Groq

Database:
Airtable

Storage:
Google Drive

Communication:
Gmail and Google Calendar

---

# Test Case 1

## Candidate

ArjunMehta(ST).pdf

## Profile Summary

Python Developer with 2 years of experience building production REST APIs using Django and Flask.

## Expected Result

Resume Extraction:
Success

Candidate Parsing:
Success

Job Match:
Strong Fit

Expected Match Score:
80–100

Application Status:
Shortlisted

Actions Expected:

* Candidate stored in Airtable
* Interview questions generated
* Interview invitation email sent
* Google Calendar event created
* Status updated to Interview Scheduled

Result:
Pass

---

# Test Case 2

## Candidate

SnehaRao(M).pdf

## Profile Summary

Java developer with limited Python exposure.

## Expected Result

Resume Extraction:
Success

Candidate Parsing:
Success

Job Match:
Possible Fit

Expected Match Score:
60–79

Application Status:
Manual Review

Actions Expected:

* Candidate stored in Airtable
* Recruiter notification email sent
* Await manual decision

Result:
Pass

---

# Test Case 3

## Candidate

RameshIyer(W).pdf

## Profile Summary

Civil engineer with no software development experience.

## Expected Result

Resume Extraction:
Success

Candidate Parsing:
Success

Job Match:
Not a Fit

Expected Match Score:
0–59

Application Status:
Rejected

Actions Expected:

* Candidate stored in Airtable
* No interview generated
* No recruiter action required

Result:
Pass

---

# Test Case 4

## Scenario

Unsupported File Upload

Input:
image.png

Expected Result:

* File ignored
* Workflow continues safely
* No Airtable record created
* No system crash

Result:
Pass

---

# Test Case 5

## Scenario

Malformed Resume

Input:
Corrupted PDF

Expected Result:

* Parsing failure handled gracefully
* Error captured
* Workflow retries triggered
* Central error handler activated

Result:
Pass

---

# Test Case 6

## Scenario

Groq API Failure

Expected Result:

* Retry mechanism executed
* Error logged
* Workflow failure captured
* No partial candidate record created

Result:
Pass

---

# Test Coverage Summary

| Module                        | Status |
| ----------------------------- | ------ |
| Gmail Trigger                 | Passed |
| Attachment Download           | Passed |
| PDF Extraction                | Passed |
| DOCX Extraction               | Passed |
| Resume Parsing                | Passed |
| JSON Validation               | Passed |
| Job Matching                  | Passed |
| Deterministic Scoring         | Passed |
| Airtable Integration          | Passed |
| Interview Question Generation | Passed |
| Email Notifications           | Passed |
| Calendar Scheduling           | Passed |
| Error Handling                | Passed |
| Unsupported File Handling     | Passed |

---

# End-to-End Workflow Validation

Resume Email
↓
Resume Extraction
↓
AI Parsing
↓
Job Matching
↓
Scoring Engine
↓
Airtable Storage
↓
Recruitment Decision
↓
Notification Workflow
↓
Calendar Scheduling

Status:
All critical workflow paths validated successfully.
