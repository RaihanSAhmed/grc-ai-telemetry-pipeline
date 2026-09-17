# GRC AI Telemetry Pipeline

An agentic governance, risk, and compliance (GRC) workflow designed to ingest mock cloud security telemetry, execute dynamic Model Context Protocol (MCP) tool calls, and generate automated, NIST-aligned risk assessments.

## Project Overview
When building modern security infrastructure, AI agents need secure, programmatic ways to query live environment data. For this project, I engineered a lightweight, end-to-end telemetry pipeline that demonstrates how an AI assistant can safely interact with underlying infrastructure to streamline cloud risk management.

## Architecture & Tech Stack
* **Orchestration:** n8n (local workflow automation)
* **Protocol & Telemetry Server:** Python, FastMCP, Server-Sent Events (SSE) transport
* **LLM Analytical Engine:** Google Gemini API
* **Environment:** Local Windows terminal development setup

---

## Implementation Phases

### Phase 1: Local FastMCP Server Setup
I began by building a local Model Context Protocol server using Python and the FastMCP framework. My goal was to create a reliable, controlled environment that could simulate cloud security telemetry on demand. By defining a custom tool called `fetch_cloud_telemetry`, I established a structured data source that mimics real-world compliance and vulnerability findings, such as unencrypted storage buckets and public internet exposure. I configured this server to run locally using Server-Sent Events, ensuring my automation platform could securely communicate with it in real time.

![FastMCP Server Terminal](Screenshot%202026-09-16%20223742.png)

### Phase 2: Orchestration and Protocol Integration
To bridge my local security telemetry with an automation workflow, I configured a local instance of n8n and utilized its native Model Context Protocol client. I established a persistent connection pointing directly to my local Python server's SSE endpoint. This layer acted as the communication bridge, allowing the system to recognize the custom telemetry tool I had programmed and query it dynamically whenever requested.

![n8n Workflow Canvas](Screenshot%202026-09-17%20000745.png)

### Phase 3: Connecting the AI Engine and Managing Workflow Logic
Next, I integrated an AI language model powered by Google Gemini to act as the analytical brain of the pipeline. Instead of manually reviewing raw security telemetry, the AI was granted secure access to call my custom local tool whenever security data was requested. During testing, I encountered an issue where the model occasionally got stuck in an infinite loop, repeatedly calling the tool instead of finishing the task. I resolved this by refining the system prompt, instructing the model to act as a rigorous risk analyst: fetch the data exactly once, parse the findings, and immediately proceed to generate a structured risk assessment.

### Phase 4: Final Execution and Risk Assessment Output
With the pipeline stable, I tested the end-to-end workflow by triggering a natural language query in the chat interface. The system successfully executed the tool call, pulled the JSON telemetry data from my local server, and translated those raw findings into a comprehensive, NIST-aligned risk assessment in just about 15 seconds. This demonstrated a fully automated path from raw security data to actionable risk management insights.

> **[ INSERT SCREENSHOT: Final chat output showing the rendered risk analysis ]**
