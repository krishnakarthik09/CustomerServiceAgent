# 🤖 AI Customer Service Agent (n8n + GPT-5-mini)

An AI-powered customer service chatbot built with **n8n**, capable of answering customer and order-related queries in real time by intelligently choosing between two different data tools — a structured database lookup and a live REST API call.

---

## 📌 Overview

This workflow simulates a real-world customer support assistant. Instead of hardcoded responses, the agent uses an LLM (GPT-5-mini) to understand user intent and decide **which tool to call** to fetch accurate, up-to-date data — without hallucinating answers.

**Example interaction:**
> **User:** What is the name of orderID 3?
> **Agent:** The employee assigned to orderID 3 is Samir. The order's customerID is 1 — tell me if you want the customer's name and I'll look it up.

---

## ⚙️ How It Works

1. **Chat Trigger** – Listens for incoming user messages.
2. **AI Agent (GPT-5-mini)** – Interprets the query using a system prompt that defines its role and tool-usage rules.
3. **Tool Selection:**
   - 🗂️ **GetCustomers** → Queries an n8n Data Table for customer records.
   - 🌐 **GetOrderData** → Calls a secured external REST API (header-based auth) for order prices, quantities, product categories, employee assignments, and order status.
4. **Simple Memory (Buffer Window)** – Retains the last 10 messages so the agent keeps context across a conversation.
5. **Response** – Agent replies conversationally, using only real retrieved data.

---

## 🧩 Workflow Architecture

```
When chat message received
        │
        ▼
     AI Agent ───────► OpenAI Chat Model (GPT-5-mini)
        │
        ├──► Simple Memory (Buffer Window, last 10 messages)
        ├──► GetCustomers (Data Table Tool)
        └──► GetOrderData (HTTP Request Tool, secured)
```

---

## 🛠️ Tech Stack

| Component | Tool/Service |
|---|---|
| Automation Platform | n8n |
| LLM | OpenAI GPT-5-mini |
| Memory | n8n Buffer Window Memory |
| Data Source 1 | n8n Data Table (Customers) |
| Data Source 2 | REST API (Order Data) with Header Auth |

---

## ✨ Key Features

- **Multi-tool reasoning** — the agent autonomously decides whether a query needs customer data, order data, or both.
- **Conversation memory** — handles multi-turn conversations naturally (e.g., follow-up questions like "what about the customer's name?").
- **Accuracy-first design** — system prompt explicitly instructs the agent not to fabricate data if it isn't found.
- **Secure API integration** — order data tool uses header-based authentication to a protected endpoint.

---

## 🚀 What I Learned

- Designing effective **system prompts** to control AI agent behavior and tool selection.
- Connecting **multiple tool types** (database vs. API) to a single LLM-powered agent.
- Implementing **memory management** for context-aware conversations.
- Debugging and validating agent responses against real execution logs.

---

## 📎 Project Type

Built as part of the **n8n Quickstart** learning track to practice building production-style AI agents with tool-calling capabilities.

---

### 🔗 Connect
Feel free to explore the workflow JSON in this repo and reach out if you have questions or suggestions!
