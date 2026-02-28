<div align="center">

# 🤖 AI Customer Support Agent (n8n Workflow)

[![n8n.io](https://img.shields.io/badge/n8n-Workflow-FF6C37?logo=n8n&logoColor=white)](https://n8n.io/)
[![OpenAI](https://img.shields.io/badge/OpenAI-Embeddings-412991?logo=openai&logoColor=white)](https://openai.com/)
[![Pinecone](https://img.shields.io/badge/Pinecone-Vector_Store-000000?logoColor=white)](https://www.pinecone.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**An intelligent, fully-automated n8n workflow that monitors a Gmail inbox, filters for customer support queries, queries a vector database (RAG) for company policies, and drafts friendly, context-aware AI responses.**

</div>

---

## 📑 Table of Contents
- [About the Workflow](#-about-the-workflow)
- [Architecture & Flow](#-architecture--flow)
- [Key Features](#-key-features)
- [Security Note](#-security-note)
- [Installation & Setup](#-installation--setup)
- [Required Credentials](#-required-credentials)
- [Contact](#-contact)

---

## 📖 About the Workflow

This repository contains an exported `Customer Support Workflow.json` file for use with [n8n](https://n8n.io/) (node-based automation). It acts as a Level-1 AI Customer Support agent for the fictional company "Deep-X". 

Instead of routing every single email to an LLM (which is cost-inefficient), the workflow utilizes LangChain classifiers to intelligently route only relevant support queries to the central AI Agent, while simply ignoring generic emails or spam.

---

## 🏗️ Architecture & Flow

The logic sequentially flows through the following nodes:

1. **Gmail Trigger**: Polls the connected inbox every 1 minute.
2. **Text Classifier (LangChain)**: Evaluates the email snippet. If it is categorized as `Other`, the workflow terminates at a `NoOp` node. If it is `Customer Support`, it proceeds to the AI.
3. **AI Agent (GPT-4o-mini)**: Hosted on OpenRouter, this Agent drives the logic. Its system prompt instructs it to be friendly, use emojis, and sign off as "Mr.X from Deep-X".
4. **Pinecone Vector Store (RAG)**: The AI Agent utilizes Pinecone as a tool to lookup internal company FAQs.
5. **OpenAI Embeddings**: Converts the inbound email search queries into numeric vectors to search Pinecone efficiently.

---

## ✨ Key Features

- **Cost-Effective Routing**: Bypasses the heavy AI Agent for non-support emails.
- **Retrieval Augmented Generation (RAG)**: Prevents LLM hallucinations by forcing the AI to retrieve factual answers from your Pinecone FAQ database.
- **Personality Driven**: Pre-configured system prompts ensure the AI replies in a warm, branded tone as "Mr.X".
- **OpenRouter Integration**: Capitalizes on the highly affordable and lightning-fast `gpt-4o-mini` model.

---

## 🔒 Security Note

This exported `.json` file is **100% safe and credential-free**. 

When n8n exports a workflow, it categorically removes all API keys, OAuth tokens, and passwords. It only retains the *internal credential ID pointers* (e.g., `"id": "OuEqCfLUUQv7PEra"`). Therefore, you can safely fork, download, or share this repository without exposing your private Pinecone or OpenRouter billing accounts.

---

## 🚀 Installation & Setup

1. **Self-Hosted or Cloud n8n**: Ensure you have an active n8n instance running.
2. **Import Workflow**:
   - Open your n8n dashboard.
   - Click **Add Workflow** -> **Import from File...**
   - Select the `Customer Support Workflow.json` file provided in this repository.
3. **Configure Credentials**: The nodes will initially show a warning because they lack your specific API keys. See the section below to connect them.

---

## 🔑 Required Credentials

To make this workflow operational on your machine, you must configure the following standard n8n integrations:

- **Gmail OAuth2**: Required for the trigger node to read incoming emails.
- **OpenRouter API**: Requires an OpenRouter account to power the LangChain Chat Models (`gpt-4o-mini`).
- **Pinecone API**: Requires your Pinecone Index/Environment details to retrieve FAQ data.
- **OpenAI API**: Required purely for the `Embeddings OpenAI` node to vectorize text.

---

## 📬 Contact

**Omar Abdelaal** - [oabdelall2004@gmail.com](mailto:oabdelall2004@gmail.com)

Project Link: [https://github.com/omarAbdelaal1/AI-Customer-Support-Agent.git]  (https://github.com/omarAbdelaal1/AI-Customer-Support-Agent.git)
