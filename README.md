# 📘 StudyBuddy Pro – AI-Powered PDF RAG + Study Planner Agent  
### *Capstone Project Submission for Kaggle x Google – 5-Day AI Agents Intensive Course*

<p align="left">
  <img src="https://img.shields.io/badge/Python-3.9+-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/Flask-API-orange?style=flat-square"/>
  <img src="https://img.shields.io/badge/AI-Multiagent-purple?style=flat-square"/>
  <img src="https://img.shields.io/badge/Multimodal-Image%20%7C%20Audio%20%7C%20Text-red?style=flat-square"/>
  <img src="https://img.shields.io/badge/Google-Gemini-brightgreen?style=flat-square"/>
  <img src="https://img.shields.io/badge/RAG-Knowledge%20Base-yellow?style=flat-square"/>
</p>
 
---

## 🏆 Competition Overview  
This project is created for the **Kaggle x Google AI Agents Intensive Course (5-Day Capstone)**.  
Participants must build an **Agent-based application** demonstrating at least **three (3)** key concepts:

- Multi-agent systems  
- Tools (built-in or custom)  
- Long-running operations  
- Sessions & memory  
- Context engineering  
- Observability  
- Agent evaluation  
- A2A Protocol  
- Agent deployment  

This project fits into the **Concierge Agents** and **Agents for Good** track categories because it helps students:

- understand their study materials  
- plan their daily or weekly study schedules  
- organize study tasks  
- optimize study habits

---

# 🎯 Project Summary  
**StudyBuddy Pro** is an **AI-powered personal study coach** that:

1. **Reads and understands any uploaded PDF** (syllabus, notes, assignments)  
2. **Uses RAG (Retrieval-Augmented Generation)** to answer questions only from the PDF  
3. **Extracts topics from the material** and turns them into actionable study tasks  
4. **Builds personalized study plans** based on time availability and user preferences  
5. Maintains **memory and session state** to track tasks and preferences over time  
6. Uses **multi-agent reasoning** to route queries to the correct sub-system (RAG or Planner)

This is a **zero-cost**, **fully local**, **tool-based**, **stateful**, and **agentic** system.

---

# 🚀 Why This Agent?
Students often struggle with:

- overwhelming amounts of unstructured study material  
- difficulty creating a structured study plan  
- not knowing which topics to prioritize  
- limited time before exams  
- needing fast, accurate explanations from their notes  

StudyBuddy Pro removes these barriers by acting as:

### ✔️ A document reader  
### ✔️ A study material expert  
### ✔️ A task generator  
### ✔️ A personalized planner  
### ✔️ A session-aware study assistant  

---

# 🧠 Core Features Implemented (Required for Judging)

## 🔧 1. **Custom Tools**
This project includes **7 fully custom tools** implemented in Python:

| Tool | Purpose |
|------|---------|
| `extract_pdf(file_path)` | Reads and extracts text from user PDF |
| `split_chunks(text)` | Splits long PDF content into manageable chunks |
| `create_embeddings(chunks)` | Generates sentence embeddings for RAG |
| `rag_search(query)` | Retrieves relevant text using FAISS vector search |
| `add_task(task, deadline)` | Adds study tasks to system memory |
| `generate_plan(num_days)` | Builds day-wise study plan based on time budgets |
| `list_tasks()` | Returns current stored tasks |

These tools allow the agent to **take actions beyond pure text generation**, satisfying the “Tools” category of the competition.

---

## 🤖 2. **Multi-Agent System**
The system is designed as a **sequential multi-agent pipeline**, even though all code runs inside one notebook.

### **Agents in the Pipeline**
1. **Intent Classifier Agent**  
   - Decides whether the user wants:  
     `PDF_QA`, `PLAN`, or `BOTH`.

2. **PDF Agent**  
   - Extracts text and prepares structured content.

3. **RAG Agent**  
   - Uses embeddings + FAISS to retrieve relevant chunks  
   - Generates grounded answers using Gemini

4. **Planner Agent**  
   - Converts PDF content into tasks  
   - Stores tasks in session state  
   - Builds personalized study plans  
   - Polishes plans using Gemini

This demonstrates **agent orchestration**, **sequential agents**, and **tool-driven decision-making**.

---

## 💾 3. **Memory**
The system maintains memory using Python state variables:

- Previously added tasks  
- User study preferences  
- Time availability  
- Difficulty levels  
- The FAISS index (document memory)  

This satisfies **Sessions & Memory** requirements.

---

## 🔁 Session & State Management

The agent holds a persistent state throughout the session, including:

- Tasks and their estimated hours  
- User constraints  
- Embeddings and vector index  
- Generated plans  

This creates a **stateful, persistent conversation** instead of a stateless LLM chat.

---

## 📊 Observability

The notebook includes debugging outputs such as:

- Tool call prints  
- Retrieved context chunks  
- FAISS index size  
- Intermediate plan structures  
- Raw vs polished schedule outputs  
- Intent classification logs  

These demonstrate **observability**, which is a required evaluation component.

---
```markdown
                         ┌───────────────────┐
                         │       User         │
                         └─────────┬─────────┘
                                   │
                        Natural Language Query
                                   ▼
                     ┌────────────────────────┐
                     │   Intent Classifier     │
                     │   (Gemini Router)       │
                     └───────┬────────┬────────┘
                             │         │
                         PDF_QA     PLAN
                             │         │
          ┌──────────────────┘         └──────────────────┐
          ▼                                                ▼
 ┌─────────────────────┐                         ┌───────────────────────┐
 │      RAG Agent      │                         │     Planner Agent     │
 │  (PDF-Grounded QA)  │                         │ (Tasks + Scheduling)  │
 └─────────┬───────────┘                         └───────────┬───────────┘
           │                                                 │
           ▼                                                 ▼
┌─────────────────────┐                         ┌────────────────────────┐
│   rag_search Tool    │                         │      Task Tools        │
│ embeddings + FAISS   │                         │  add / list / plan     │
└──────────┬──────────┘                         └──────────┬────────────┘
           │                                                 │
           └──────────────────────┬──────────────────────────┘
                                  ▼
                       Final Combined Response
```
---

## 🛠 Technologies Used

| Component | Technology |
|-----------|------------|
| **LLM** | Gemini 2.0 Flash |
| **RAG** | SentenceTransformers + FAISS |
| **PDF Ingestion** | PyPDF |
| **Agent Logic** | Custom Python tools & multi-agent routing |
| **Notebook Environment** | Google Colab / Kaggle |
| **Memory** | In-notebook Python state |
| **Multi-Agent Routing** | Gemini classifier |

---

## 🎬 Demo Workflow

### **Example 1 — PDF Q&A**
**User:**  
“Explain gradient descent from my notes.”

**Agent:**  
- Retrieves top 5 chunks  
- Answers only using PDF content  

---

### **Example 2 — Study Plan**
**User:**  
“Make a 7-day study plan based on my syllabus, I can study 2 hours per day.”

**Agent:**  
- Extracts tasks from PDF  
- Distributes tasks into days  
- Applies user preferences  
- Creates a polished weekly schedule  

---

### **Example 3 — Combined**
**User:**  
“Explain SVM and also create a 3-day plan to revise it.”

**Agent:**  
- Runs RAG Agent → explains SVM  
- Runs Planner Agent → builds revision plan  
- Returns combined output  

---

## 📝 How To Run the Notebook

1. Upload a PDF (syllabus or notes)  
2. Run the embedding + FAISS setup  
3. Interact using:

```python
studybuddy_agent("your question or request", num_days=7, hours_per_day=2)
```
### 🔧 Customize:

You can customize the agent behavior using the following parameters:

- **num_days** — Number of days to generate the study plan  
- **hours_per_day** — How many hours the user can study each day  
- **preferences** — Any study preferences (e.g., “I study at night”, “Do light topics first”)  

---

## 🎯 Value of This Project

**StudyBuddy Pro** automates what students struggle with most:

- Understanding long, dense PDFs  
- Breaking topics into actionable tasks  
- Creating personalized schedules  
- Staying consistent with study goals  

It dramatically reduces planning time and transforms passive documents into **actionable learning workflows**.

---

## 📈 Future Improvements

- Add calendar integration (Google Calendar API)  
- Add long-term memory (persistent vector DB storage)  
- Add difficulty modeling + spaced repetition  
- Allow multiple PDFs (merge, unify topics, cross-reference)  
- Deploy as a web or mobile application  

---

## 👨‍💻 Author

**Rohan Rathod**  
*MCA Student • AI/ML Developer • Agent Systems Enthusiast*
<table style="width:100%;border-collapse:collapse;font-size:16px;">
  <tr>
    <td style="padding:8px 0;"><b> Author</b></td>
    <td>Rohan Rathod</td>
  </tr>
  <tr>
    <td style="padding:8px 0;"><b>📧 Email</b></td>
    <td><a href="mailto:mukthanjalibonala@gmail.com">rohanrathod.dev@gmail.com</a></td>
  </tr>
  <tr>
    <td style="padding:8px 0;"><b>💼 LinkedIn</b></td>
    <td><a href="https://www.linkedin.com/in/rohan-rathod-49253a36a/">View Profile</a></td>
  </tr>
  <tr>
    <td style="padding:8px 0;"><b>📊 Kaggle</b></td>
    <td><a href="">Live Notebook</a></td>
  </tr>
  <tr>
    <td style="padding:8px 0;"><b>📝 Write-up</b></td>
    <td><a href="">View Writeup</a></td>
  </tr>
</table>
</div>

---

## 🏁 Conclusion

This project demonstrates the power of **Agents**, **Tools**, **RAG**, **Memory**, and **Stateful Reasoning** in a single, cohesive workflow that solves a real problem faced by students.

**StudyBuddy Pro = AI that understands your notes + plans your success.**
