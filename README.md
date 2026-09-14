# abtaal-el-digital
CodeRefine Qualification 2 - Carieeer

Link:
https://excalidraw.com/#json=YpXuRbMvwjX-KMQVtEoyv,nhTayJb00EBPqsxL_SRxFw

Functional Requirements:
User profiles: Candidate make profile. He put his skill and education. Employer make company profile too.

Job posts: Employer add new job. He write the skills he want. He put budget also.

Matching: System find good jobs to candidate. System find good candidates to employer.

Applications: Candidate apply for job. Employer change the status. Status can be apply, interview or reject. System not allow apply two time.

Skill gap: System compare candidate skill and job. It tell candidate what missing skill he need.

Search: Candidate search job by keyword and money. Employer search candidate by experience.

Notifications: System send notification. It send email if status change or new match.


Non-Functional Requirements:
High availability: System need to work all time. We want 99.99% uptime. If system down, the hiring stop.

Scalability: System must handle big traffic. If many user come in same time, system must not crash.

Low latency: System must be fast. Search and match must take less than 200ms.

Strict consistency: Data must be strict and correct. When user apply or status change, system save it right so no wrong data happen.


API Designe:

1. Create a Job 

Endpoint: POST /api/v1/jobs

Headers: Authorization: Bearer <EmployerToken>

Request Body:

JSON
{
  "title": "Backend Engineer",
  "description": "java , soft sKills, problem solveing and System designe",
  "skills": ["Java", "Spring Boot", "System designe"]
}
Response 201 Created : 

JSON
{
 "job_id": "uuid-1234", "status": "PUBLISHED" 
}

2. Search Jobs

Endpoint: GET /api/v1/jobs/search?title=Backend Engineer&skills=Java,Spring Boot and System Designe

Response 200 OK:

JSON
{
  "total_results": 150,
  "jobs":
 [ 
    {
       "job_id": "uuid-1234",
       "title": "Backend Engineer" 
    }

 ]
}


3. Apply to a Job 

Endpoint: POST /api/v1/applications

Headers: Idempotency-Key: <UUID>

Request Body: { "job_id": "uuid-1234", "cover_letter": "hi, ..... etc" }

Response (201 Created): 

JSON
{ 
    "application_id": "app-1234", 
    "status": "APPLIED"
}


4. Skill-Gap Analysis

Endpoint: GET /api/v1/candidates/{candidate_id}/skill-gaps/{job_id}

Response 200 OK:

JSON
{
  "match_percentage": "87%" ,
  "matched_skills": ["Java", "PostgreSQL"],
  "missing_skills": ["Kubernetes"]
}
