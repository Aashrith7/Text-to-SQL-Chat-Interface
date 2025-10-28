# 💬 Text-to-SQL Chat Interface using GPT-4 and Mistral AI

Welcome! 👋  
This project shows how to build an **AI-powered SQL chatbot** that lets you ask questions about your **MySQL database using plain English** — and get real answers back!  

It combines the reasoning power of **OpenAI’s GPT-4** (and **Mistral AI** as an alternative model) with a **Streamlit** user interface.  
The chatbot automatically converts your question into a valid **SQL query**, runs it on your database, and explains the results in easy-to-understand language.

---

## 🎯 Project Overview

This project demonstrates how **Large Language Models (LLMs)** can help users interact with databases without knowing SQL.  
By using **LangChain**, we connect the LLM with a real database — so when you ask something like:

> “Show me the top 5 customers by total purchases.”

The app:
1. Reads your database structure (schema).  
2. Generates the correct SQL query automatically.  
3. Executes it on MySQL.  
4. Returns a short, clear summary of the results.

---

## 🧠 Key Features

- 🗣️ **Natural Language Queries** — Talk to your database in plain English.  
- 🧩 **Automatic SQL Generation** — GPT-4 or Mistral creates optimized queries for you.  
- ⚙️ **Real Database Connection** — Fetches real data using MySQL and SQLAlchemy.  
- 🎨 **Streamlit GUI** — Clean, easy-to-use chat interface.  
- 🔄 **Context Memory** — Remembers the chat so you can ask follow-up questions.  
- 🧠 **AI-Powered Explanations** — Converts raw SQL results into understandable summaries.

---

## 🧩 How It Works

The chatbot performs two main steps behind the scenes:

### 1️⃣ SQL Generation
The LLM (GPT-4 or Mistral) reads:
- The **database schema** (table names and columns),
- The **conversation history**, and
- Your **new question**.

It then predicts the correct SQL query to answer your question.

### 2️⃣ Answer Generation
Once the SQL query runs successfully, the model takes:
- The **query**,  
- The **raw SQL result**, and  
- The **context of your question**,  

and writes a short, natural explanation of the answer — for example:  
> “The customer **John Smith** spent the most with a total of **$5,230**.”

---

## 🧭 System Architecture

```mermaid
flowchart LR
    A[User Question] -->|Streamlit| B[SQL Generation Prompt]
    B -->|LLM (GPT-4 or Mistral)| C[Generated SQL Query]
    C -->|SQLAlchemy| D[MySQL Database]
    D --> E[SQL Result]
    E --> F[Answer Synthesis Prompt]
    F -->|LLM| G[Natural Language Answer]
    G -->|Displayed via Streamlit| A
