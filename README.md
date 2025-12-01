### 1. Executive Summary
In the public sector, the manual verification of citizen applications for schemes (such as welfare, housing, or health) is a bottleneck that causes significant delays and administrative burden. This project proposes a **Multi-Agent System** designed to automate the intake, scrutiny, and decision-making process for government applications. By leveraging **Google's Gemini 2.0 Flash** and Vertex AI, the system will reduce processing time from days to seconds while providing applicants with instant, transparent feedback on rejections.

### 2. Problem Statement
Government schemes, such as the Ayushman Bharat Yojana, receive millions of applications annually. The current manual processing workflow faces three critical issues:
* **High Latency:** Officers must manually open every file, verify details against physical rules, and cross-check data. This leads to massive backlogs.
* **Lack of Granular Feedback:** When an application is rejected, the applicant often receives a generic status like "Rejected" without knowing why. (e.g., Was the photo blurry? Was the income certificate expired?)
* **Resubmission Loops:** Due to the lack of clear feedback, applicants often reapply with the same errors, further clogging the system.

### 3. Proposed Solution: The Multi-Agent Architecture
We propose an "Agentic" workflow where specialised AI agents collaborate to handle the verification process. This approach mimics a human team, where different officers handle different parts of the scrutiny.
**The Agent Team**
* **Agent A: The Orchestrator (Manager)**
Controls the workflow. It receives the application, delegates tasks to specialised agents, and compiles the final decision.
* **Agent B: The Document Analyst (Vision)**
Uses **Multimodal AI** to "see" the uploaded documents. It performs OCR, checks for document validity (e.g., "Is this actually an Aadhaar card?"), and detects quality issues (blur/cuts).
* **Agent C: The Compliance Officer (Logic)**
The "Brain" of the operation. It cross-references the data extracted by Agent B against the scheme's eligibility rules (e.g., "Is Income < ₹5 Lakhs?").
* **Agent D: The Communication Liaison (Response)**
Translates technical rejection codes into polite, actionable advice for the citizen in their local language.

### 4. The WorkFlow
**Eg Scenario:** An applicant, Mr Sharma, applies for the health scheme. He fills out the form stating his income is ₹4 Lakhs, but accidentally uploads an expired Income Certificate.

* **Submission:** Mr Sharma submits his form and uploads Income_Cert.jpg.
* **Agent B (Analyst) Scans:**
    * Observation: "Document detected: Income Certificate."
    * Extraction: "Issue Date: Jan 2019. Validity: 3 Years."
    * Flag: "Document Validity Expired."
* **Agent C (Compliance) Reviews:**
    * Rule Check: "Scheme requires a valid certificate issued within the last 12 months."
    * Decision: "REJECT. Reason Code: DOC_EXPIRED."
* **Agent D (Communication) Drafts Response:**
    * Output to User: "Namaste, Mr Sharma. Your application was not accepted because your Income Certificate is from 2019. Please visit your local Tehsil office to get a current certificate and re-apply."
* **Result:** The application is rejected in real-time (30 seconds), and Mr Sharma knows exactly what to fix.

![Multi agents working flow](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F11573631%2Fafb1ab9fc8372045571ccec57321e21a%2FScreenshot%202025-11-20%20101328.png?generation=1764587052760631&alt=media)

### 5. Why agents?
We chose an Agentic Workflow because verification requires distinct cognitive skills that mimic a human team. A simple script cannot handle the diverse tasks required:
1. Visual Perception: To extract data from unstructured images (documents).
2. Logical Reasoning: To apply complex eligibility rules.
3. Communication: To translate technical logic into empathetic, local-language advice. Agents allow us to separate these concerns into specialized, reliable components (Analyst, Compliance, Communication).

### 6. Technical Stack & Tools
This project utilises the Google Cloud Ecosystem as learned in the "AI Agents Intensive" course.

* **Core Model:** Gemini 2.0 Flash.
    * **Reasoning:** Selected for its high speed, low cost, and native Multimodal capabilities (processing images/PDFs without external OCR tools).
* **Orchestration:** LangGraph or Google Agent Development Kit (ADK).
    * **Reasoning:** To manage the state and hand-offs between the Analyst and Compliance agents.
* **Frontend:** Streamlit.
    * **Reasoning:** To provide a simple, user-friendly interface for file uploads.
* **Knowledge Base:** RAG (Retrieval Augmented Generation).
    * **Reasoning:** To store the specific PDF rulebooks of the government schemes so the Compliance Agent can look up eligibility criteria dynamically
