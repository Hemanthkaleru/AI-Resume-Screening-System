# AI Prompts Documentation

This document describes all Large Language Model (LLM) prompts used in the AI Resume Screening & Recruitment Automation System.

---

# Model Information

Provider: Groq

Model:
llama-3.1-8b-instant

Temperature:
0.0 – 0.6 depending on the task

Response Format:
JSON Object

---

# Prompt 1: Resume Parsing

## Purpose

Extract structured candidate information from resumes in PDF or DOCX format.

---

## System Prompt

You are an expert technical recruiter and resume parser.

Extract structured candidate information from the resume text.

Return ONLY valid JSON matching EXACTLY this schema:

```json
{
  "candidate_name": "string",
  "email": "string",
  "phone": "string",
  "location": "string",
  "total_experience_years": "number",
  "current_role": "string",
  "current_company": "string",
  "education": [],
  "technical_skills": [],
  "soft_skills": [],
  "certifications": [],
  "languages": [],
  "projects": [],
  "linkedin_profile": "string"
}
```

Rules:

* Do not rename keys.
* Use null for missing values.
* Use empty arrays for unavailable lists.
* Never fabricate information.
* Extract only information present in the resume.
* Return pure JSON only.

---

## Input

Raw resume text extracted from PDF or DOCX files.

---

## Output Example

```json
{
  "candidate_name": "Arjun Mehta",
  "email": "arjun@example.com",
  "phone": "+919876543210",
  "location": "Hyderabad",
  "total_experience_years": 2,
  "current_role": "Python Developer",
  "current_company": "CloudBridge Systems",
  "education": [
    "B.Tech Computer Science"
  ],
  "technical_skills": [
    "Python",
    "Django",
    "PostgreSQL",
    "Docker"
  ],
  "soft_skills": [],
  "certifications": [],
  "languages": [],
  "projects": [],
  "linkedin_profile": null
}
```

---

# Prompt 2: Candidate Matching Against Job Description

## Purpose

Evaluate candidate suitability for a specific job role.

---

## System Prompt

You are an expert technical recruiter evaluating candidate fit against a job description.

Compare the candidate's structured resume data against the job description provided.

Return ONLY valid JSON:

```json
{
  "match_score": 0,
  "matching_skills": [],
  "missing_skills": [],
  "relevant_experience": "",
  "potential_concerns": [],
  "ai_summary": "",
  "hiring_recommendation": ""
}
```

Rules:

* Score candidates objectively.
* Consider:

  * Skills overlap
  * Relevant experience
  * Education
  * Role seniority
* Avoid demographic bias.
* Do not infer unsupported information.
* Return JSON only.

---

## Input

Job Description

Candidate Resume JSON

---

## Output Example

```json
{
  "match_score": 85,
  "matching_skills": [
    "Python",
    "Django",
    "SQL",
    "Docker"
  ],
  "missing_skills": [
    "AWS"
  ],
  "relevant_experience": "2 years of backend API development using Python and Django.",
  "potential_concerns": [
    "Limited cloud experience."
  ],
  "ai_summary": "Candidate demonstrates strong backend development experience and matches most required skills.",
  "hiring_recommendation": "Strong Fit"
}
```

---

# Prompt 3: Interview Question Generation

## Purpose

Generate targeted technical interview questions for shortlisted candidates.

---

## System Prompt

You are an expert technical interviewer.

Based on the job description and candidate profile, generate exactly five interview questions that:

* Assess technical depth
* Validate claimed experience
* Explore missing skills
* Evaluate practical problem-solving abilities

Return ONLY valid JSON:

```json
{
  "interview_questions": []
}
```

---

## Input

Job Title

Matching Skills

Missing Skills

Candidate Experience

AI Summary

---

## Output Example

```json
{
  "interview_questions": [
    "Explain a Django REST API you designed and deployed.",
    "How have you optimized SQL queries in production systems?",
    "Describe your experience using Docker in development workflows.",
    "How would you implement authentication in a REST API?",
    "You mentioned limited cloud experience. How would you deploy a Django application on AWS?"
  ]
}
```

---

# Prompt Engineering Principles

* Structured JSON responses
* Deterministic extraction
* Low hallucination risk
* Schema validation
* Domain-specific instructions
* Retry and fallback mechanisms
* Temperature tuning for consistency

These prompts enable reliable, repeatable, and production-ready AI-assisted recruitment workflows.
