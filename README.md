# 🧠 Text-to-SQL Chat Interface — Natural Language MySQL Q&A (Streamlit + LangChain)

Ask questions in plain English and get **auto-generated SQL** plus a **natural-language explanation** of results — all from your **MySQL** database.  
Built with **Streamlit**, **LangChain**, **OpenAI**, and **SQLAlchemy**.

---

## ✨ Features

- **NL → SQL**: Generates safe, schema-aware SQL from your question
- **Context-aware**: Uses recent chat history to refine follow-ups
- **Explains results**: Turns table outputs into clear summaries
- **Plug-and-play**: Works with any MySQL schema via connection settings
- **Streamlit UI**: Simple chat interface; connect from the sidebar

---

## 🧠 How it works

Under the hood there are **two chained LLM steps**:

1) **SQL Generation Chain**  
   - Prompt includes: *database schema* + *chat history* + *user question*  
   - LLM outputs **only** SQL (no extra text).

2) **Answer Synthesis Chain**  
   - Executes the SQL via `SQLDatabase.run(...)`  
   - Prompt includes: *schema* + *question* + *SQL query* + *SQL response*  
   - LLM returns a clear, human-readable answer.

```mermaid
flowchart LR
    U[User Question] -->|Streamlit| A[SQL Generation Prompt]
    A -->|LLM (OpenAI or Groq)| Q[SQL Query]
    Q -->|SQLAlchemy| DB[MySQL Database]
    DB --> R[Tabular Result]
    R --> B[Answer Synthesis Prompt]
    Q --> B
    B -->|LLM| NL[Natural Language Answer]
    NL -->|Streamlit| U

