# Project Roadmap: Smart Campus Helpdesk with Agentic AI

## PHASE 1: Requirements & Setup

### Goals:
- Agents communicate with each other (MCP style)
- Run locally using Ollama or LM Studio (offline LLMs)
- Users interact via a chat interface
- Agents pull data from a real database
- Modular, so more agents can be added later

### Tools Needed:
- Python: Agent logic & backend
- FastAPI or Flask: API backend
- SQLite or MongoDB: Database
- Ollama / LM Studio: Running LLMs locally
- React.js or HTML/JS: Chat frontend
- LangChain (optional): Agent chaining
- Postman: For API testing
- VSCode: Development

---

## PHASE 2: Agent Design

### Agents:
1. **OrchestratorAgent** - Routes queries to correct agent
2. **AcademicAgent** - Handles class schedules, subjects, exams
3. **FinanceAgent** - Handles fees, payments, due dates
4. **EventAgent** - Handles events, workshops, fests

### MCP-style Message Format (JSON):
```json
{
  "sender": "OrchestratorAgent",
  "receiver": "AcademicAgent",
  "action": "get_exam_schedule",
  "data": {"student_id": "CU2025AI001"}
}
```

---

##  PHASE 3: Database Design

Use **SQLite or MongoDB**.

### Example Tables:
- `courses(id, name, instructor, schedule)`
- `fees(student_id, amount_due, due_date)`
- `events(id, title, date, description)`
- `users(student_id, name, email)`

---

##  PHASE 4: Backend + Agent Logic

Use **FastAPI** with endpoints:

- `/chat (POST)` → OrchestratorAgent
- `/academic` → AcademicAgent
- `/finance` → FinanceAgent
- `/events` → EventAgent

Each agent:
- Parses MCP messages
- Queries DB
- Returns JSON response

---

## PHASE 5: LLM Integration (Ollama / LM Studio)

Use Ollama’s HTTP API with models like `mistral`, `gemma`.

### Example:
```python
import requests

def call_ollama(prompt):
    response = requests.post("http://localhost:11434/api/generate", json={
        "model": "mistral",
        "prompt": prompt
    })
    return response.json()["response"]
```

---

## PHASE 6: Chat Interface

### Tech Stack:
- React.js or HTML/JS

### UI Components:
- TextBox for input
- Message bubbles
- Agent avatars
- Display chat log

### Flow:
Frontend posts user input to `/chat` → response displayed in UI

---

## PHASE 7: Communication Flow

1. User types a question
2. Frontend sends to `/chat` (OrchestratorAgent)
3. Orchestrator uses LLM to decide target agent
4. Sends MCP message to agent
5. Agent queries DB and replies
6. Orchestrator formats response
7. Frontend displays it

---

## PHASE 8: Optional Features

- Voice input via Web Speech API
- Add new agents (e.g., LibraryAgent)
- Save chat history
- User login system
- LangChain for agent chaining

---

## Folder Structure

```
/smart-campus-helpdesk
├── backend/
│   ├── main.py
│   ├── agents/
│   │   ├── orchestrator.py
│   │   ├── academic_agent.py
│   │   ├── finance_agent.py
│   │   └── event_agent.py
│   ├── database/
│   │   ├── db.py
│   │   └── models.py
│   └── utils/
│       └── ollama.py
├── frontend/
│   └── chat-ui/
├── requirements.txt
└── README.md
```

---

## Learning Outcomes

- Build and deploy multi-agent architecture
- Route messages using MCP
- Run offline LLMs via Ollama/LM Studio
- Build real-time chat interface
- Master DB + API integration
