# Operational Copilot

AI-powered COO layer for early-stage startups. Simulates multi-agent orchestration, digital twins, synthetic user personas, and real-time ops analytics — all in a single interactive dashboard.

Built as a hackathon submission for the Agentic AI track.

---

## What it does

Early-stage D2C founders spend 15+ hours a week on manual operations — checking ad spend, monitoring inventory, responding to customers, and making decisions on gut feel rather than data. Operational Copilot is a prototype of an autonomous AI layer that handles this continuously in the background.

The system is designed around four layers that work together:

- A **data and simulation layer** that ingests orders, ad performance, and inventory into a live digital twin of the business
- An **agentic orchestration layer** running a multi-agent loop (Orchestrator, Supplier Agent, Customer Service Agent) that observes signals, reasons about them, and acts autonomously
- An **execution and analysis layer** that calls external APIs, runs ROI calculations, and generates alerts
- A **dashboard frontend** that surfaces everything in real time — agent thought traces, KPI trends, self-correction logs, and scenario simulations

A cross-layer synthetic user generator creates LLM-powered customer personas with configurable buy, churn, and complaint probabilities, used to simulate campaign outcomes before spending real budget.

---

## Architecture

```
Layer I   — Data & Simulation
           RAG pipeline (PyMuPDF, ChromaDB, text-embedding-ada-002)
           Digital Twin Engine (Pandas state model, SQLite, rules YAML)

Layer II  — Agentic Orchestration
           LangGraph + Llama 3 (Groq) + StateGraph
           Agents: Orchestrator, Supplier, Customer Service
           Execution: RAG retrieval, ReAct tool calls, TAO loop

Layer III — Execution & Analysis
           Internal: DB query tools, KPI calculator, audit logger
           External: Slack webhook, Email (SMTP), REST connectors
           Analytics: ROI engine, scenario diff, report gen

Layer IV  — Dashboard Frontend
           Streamlit + WebSocket + st.session_state
           Panels: live interaction feed, twin state display,
                   revenue chart, self-correction log, thought trace

Cross-layer — Synthetic Users & Agent Interaction Bus
           Claude / LLM personas, persona YAML config
           Redis Pub/Sub: event routing, state sync, message queuing
```

---

## Prototype

The prototype in this repo (`index.html`) is a fully self-contained frontend simulation of the system. No backend is required to run it.

It includes:

- Live agent thought trace streaming with Orchestrator, Supplier, and Customer Service agents cycling through the TAO (Think-Act-Observe) loop
- KPI cards that update in real time — revenue, CAC, inventory level, churn risk
- Digital twin state bars reflecting ad spend, fulfillment rate, stockout risk, and campaign ROI
- A 7-day revenue trend chart
- Scenario diff simulator — drag an ad spend multiplier and see projected revenue, margin, and stockout risk recalculate instantly
- Synthetic user persona panel with configurable buy, churn, and complaint probabilities
- Agent interaction bus showing Redis-style event routing between agents
- Self-correction log showing when the agent revises its own estimates
- A data input drawer where you can enter your own business numbers and have everything update to reflect them

---

## Running it

No install required. Open `index.html` in any modern browser.

Or visit the live demo at: `(https://insvanshu.github.io/Operational-Co-pilot/)`

---

## Entering your own data

Click **Enter your data** in the top-right of the dashboard. The drawer lets you input:

- Business name and vertical
- Daily revenue, ad spend, CAC, and campaign ROAS
- Inventory level, order fulfillment rate, churn rate
- 7-day revenue history (populates the chart)
- Customer segment names and buy / churn probabilities

Hit **Apply to Dashboard** and all panels update live. The agent trace logs the data ingestion event as part of the simulated agentic loop.

---

## Tech stack (prototype)

- Vanilla HTML / CSS / JavaScript
- Chart.js for the revenue trend chart
- JetBrains Mono + Syne + Inter via Google Fonts

The full production architecture (described above) would be built on LangGraph, Groq, ChromaDB, Streamlit, Redis, and SQLite.

---



MIT
