# AI Career Fit Analyzer

An automated **n8n workflow** that analyzes a user's resume against a target job description or evaluates it against predefined role benchmarks to identify suitable career opportunities and skill gaps.

## Overview

The workflow provides two different resume analysis paths.

When a user provides a specific job description, the workflow compares the submitted resume directly against the requirements of that job and generates a detailed analysis.

When no specific job description or target role is provided, the workflow analyzes the resume against predefined career benchmarks and suggests suitable roles based on the applicant's skills and experience.

The results are delivered to the user through email.

## Workflow

```text
                    Resume Submission
                          │
                          ▼
                       Webhook
                          │
                          ▼
                    PDF Extraction
                          │
                          ▼
                    Data Cleaning
                          │
                          ▼
              ┌───────────┴───────────┐
              │                       │
       Job Description          No Target Role
          Provided?                   │
              │                       ▼
              ▼                 Role Matching
        AI Job Fit Analysis           │
              │                       ▼
              │                 Role Benchmark
              │                       │
              │                       ▼
              │                 AI Career Analysis
              │                       │
              └───────────┬───────────┘
                          ▼
                    Parse Results
                          │
                          ▼
                    Email Results
```

## Features

* Accepts resume submissions through a webhook
* Extracts text from PDF resumes using PDF.co
* Cleans and processes extracted resume data
* Supports analysis against a specific job description
* Provides predefined benchmarks for multiple technology roles
* Calculates a resume-to-job fit score
* Identifies matching skills
* Identifies missing skills
* Highlights weaknesses and experience gaps
* Provides actionable improvement suggestions
* Suggests alternative career roles when applicable
* Generates an overall assessment
* Delivers the analysis results through email

## Analysis Modes

### 1. Job Description Analysis

When a user provides a specific job description, the workflow compares the resume directly against the provided requirements.

The AI generates:

* **Match Score** — A score from 0–100
* **Matching Skills** — Skills found in both the resume and job requirements
* **Missing Skills** — Relevant skills not found in the resume
* **Weaknesses** — Identified areas of weakness with potential improvement suggestions
* **Suggestions** — Actionable recommendations for improving job fit
* **Experience Gaps** — Potential gaps between the resume and the role
* **Overall Assessment** — A summary of the candidate's fit for the position

### 2. Career Role Analysis

When no specific target role is provided, the workflow evaluates the resume against predefined career benchmarks.

The AI can:

* Identify suitable career roles
* Assign fit scores to suggested roles
* Explain why each role may be suitable
* Identify the candidate's resume strengths
* Provide general improvement recommendations

## Supported Career Benchmarks

The workflow currently includes predefined benchmarks for:

* Backend Developer Intern
* Frontend Developer Intern
* Full Stack Developer Intern
* Python Developer Intern
* Data Analyst Intern
* Machine Learning Intern
* AI Engineer Intern
* DevOps Engineer Intern
* Cybersecurity Intern
* QA Engineer Intern

Each benchmark includes:

* Required skills
* Preferred skills
* Typical experience level
* Common tools

You can add/remove benchmarks as per your needs.

## Example Benchmark Structure

A role benchmark is structured around four categories:

```text
Role
├── Required Skills
├── Preferred Skills
├── Typical Experience
└── Common Tools
```

This allows the workflow to compare a candidate's resume against a consistent role-specific reference point.

## Email Output

The analysis is delivered to the user's email address and includes the relevant results for the selected analysis mode.

For job-specific analysis, the email contains:

* Fit score
* Matching skills
* Missing skills
* Weaknesses
* Suggestions
* Alternative roles
* Overall assessment

For general career analysis, the email can include:

* Alternative career roles
* Fit scores
* Role-specific reasoning
* Resume strengths
* General improvement recommendations

## Workflow Components

| Node             | Purpose                                                      |
| ---------------- | ------------------------------------------------------------ |
| Webhook          | Receives resume and analysis information                     |
| PDF.co API       | Extracts text from the submitted PDF resume                  |
| Merge            | Combines webhook and extracted resume data                   |
| Data Cleaning    | Cleans and formats resume and job description text           |
| If               | Determines whether a job description is available            |
| AI Agent         | Analyzes the resume against a specific job description       |
| Role Check       | Determines whether a target role is available                |
| Benchmarks       | Matches the target role against predefined career benchmarks |
| AI Agent1        | Performs benchmark-based career fit analysis                 |
| Groq Chat Model  | Provides the language model for job-specific analysis        |
| Groq Chat Model1 | Provides the language model for career benchmark analysis    |
| Output Parsing   | Converts AI-generated JSON into structured workflow data     |
| Output Parsing1  | Parses benchmark analysis results                            |
| Send an Email    | Delivers job-specific analysis results                       |
| Send an Email1   | Delivers career fit analysis results                         |

## Technologies Used

* **n8n** — Workflow automation
* **PDF.co** — Resume PDF text extraction
* **Groq** — AI model provider
* **Llama 3.3 70B** — Language model used for resume analysis
* **SMTP** — Email delivery

## Project Purpose

This project demonstrates an AI-powered resume analysis and career matching workflow that can evaluate candidates against specific job descriptions or predefined career benchmarks.

It combines document processing, data cleaning, conditional workflow logic, AI-powered analysis, structured JSON processing, role benchmarking, and automated email delivery into a single n8n workflow.
