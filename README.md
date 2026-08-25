# Job Scoring AI: AI-Powered Job Screening Automation

A job scoring system built as an AI skill for Claude (Anthropic), developed for a client applying for positions in the Canadian market.

## Why this is an AI integration project

This is not simply a case of using an AI API to generate text. The system automates a repetitive decision-making process.

The client was actively searching for jobs and needed to evaluate each position against specific criteria before deciding whether it was worth applying. Doing this manually for every job was time-consuming and made the evaluation inconsistent.

The solution connects an AI model to this process. The user provides a job description, the system evaluates it using predefined criteria, and returns a structured result that can be compared with other opportunities.

## Problem

Candidates often evaluate job opportunities based on several factors, such as technical fit, career alignment, compensation, company quality, and location.

When this is done manually across many job postings, the criteria can be applied inconsistently. A position evaluated one day may be judged differently from a similar position evaluated several days later.

The process also becomes difficult to maintain when the number of opportunities increases.

## Solution

An AI skill that receives a Job Description pasted into the chat and evaluates it using 5 main criteria.

The output always follows the same structure, making it easier to compare different job opportunities using the same evaluation standard.

### The 5 criteria

| # | Criterion          | What it measures                                                                                             |
| - | ------------------ | ------------------------------------------------------------------------------------------------------------ |
| 1 | Requirements Match | Technical alignment between the requirements of the position and what the candidate can demonstrate          |
| 2 | Profile Match      | Alignment between the candidate's career path and the position                                               |
| 3 | Compensation       | Salary range for the position, including external research when compensation is not provided                 |
| 4 | Company Quality    | The company's relevance as a career opportunity, based on external research                                  |
| 5 | Location           | Quality of life in the city or region where the position is located, based on a public cost-of-living source |

### Design decisions

* **Anti-hallucination rules:** The system does not create experience, certifications, or responsibilities that the candidate has not demonstrated. Missing information is classified as "Not Demonstrated" instead of being treated as a lack of experience.

* **Substance vs. terminology:** The system checks whether a competency is actually missing or simply described using different terminology. This prevents the candidate from being penalized because the job description and their experience use different terms for similar skills.

* **Semantic matching:** The system identifies functional similarities between terminology used in different industries and markets instead of relying only on exact keyword matches.

* **Conditional external research:** External research is only performed when required for a specific criterion. The system follows a defined order: explicit information, company data, market data for the role, and general market data as a fallback. The source level used in the evaluation is also identified.

* **Single source per research criterion:** Each research-based criterion uses one consistent external source. This avoids combining data from sources with different methodologies and reduces the need for the AI to reconcile conflicting information.

* **Calibration benchmarks:** Subjective criteria such as company quality and location use predefined reference points. This helps keep scores consistent across different evaluations.

* **Fixed scoring scale:** Scores are given in 0.5 increments to avoid unnecessary precision in a qualitative evaluation.

* **No final combined score:** The system keeps the 5 scores separate instead of producing a single recommendation. The final decision about whether to apply remains with the candidate.

## Example

**Input:** A Job Description for a Project Coordinator position pasted into the chat.

**Output:**

| Criterion          | Score |
| ------------------ | ----- |
| Requirements Match | 4.0   |
| Profile Match      | 4.5   |
| Compensation       | 3.0   |
| Company Quality    | 3.5   |
| Location           | 3.5   |

The system can also provide conditional warnings when relevant, such as identifying the source used to estimate compensation when the salary is not included in the job posting or highlighting relevant gaps between the position and the candidate's profile.

## Stack

* **Claude (Anthropic):** AI model and skills system
* **Structured prompt engineering:** Conditional rules, interpretation priorities, and a fixed output format
* **Conditional external research:** Public sources for salary and cost-of-living data

## Result

The process of deciding whether a job was worth applying for became faster and more consistent. The system reduced the variation that naturally occurs when evaluating multiple opportunities manually.

---

*The client's name, numerical benchmarks, and internal calibration rules have been omitted or replaced with illustrative versions for confidentiality. The architecture, decision logic, and output format described here are the same as those used in production.*
