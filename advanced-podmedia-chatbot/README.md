# Advanced AI Chatbot for Customer Support & Calendly Booking (PodMedia)

This project is a complete, production-ready chatbot solution designed for PodMedia. It features an advanced, multi-tool AI agent named "John" that serves as a customer support assistant and a meeting scheduler. The system is comprised of two distinct workflows: a pipeline for ingesting knowledge and the main, customer-facing chatbot application.

## 🎯 Goal & Purpose

The goal is to provide a seamless, intelligent, and friendly user experience for PodMedia's customers. The chatbot can answer detailed questions, check real-time meeting availability, and book meetings directly through Calendly, all while maintaining conversation history and supporting multiple languages.

## 🏛️ System Architecture

The solution is split into two parts for clean separation of concerns:

1.  **Knowledge Base Ingestion:** A one-time, manually run workflow that prepares the bot's knowledge by processing a Google Doc and storing it in a searchable vector database.
2.  **The Chatbot Application:** The main, event-driven workflow that interacts with users, uses multiple tools to perform tasks, and provides intelligent responses.

---

### Part 1: The Knowledge Base Ingestion Workflow

This preparatory workflow is responsible for populating the bot's brain.

**Process:**
* **Downloads** a Google Doc containing the PodMedia FAQs.
* **Loads & Chunks** the document into smaller, manageable pieces.
* **Embeds** the text chunks into numerical vectors using OpenAI.
* **Stores** these vectors in a Pinecone vector database for fast and efficient semantic search.

### Part 2: The Customer-Facing Chatbot

This is the core application—a powerful AI agent equipped with a suite of tools to handle complex user requests.

**Key Features:**
* **Multi-Tool AI Agent:** The chatbot is a single agent that can intelligently decide which tool to use based on the user's request.
* **RAG for Factual Answers:** It connects to the Pinecone knowledge base (created in Part 1) to provide accurate, context-aware answers to questions about PodMedia.
* **Real-Time Calendly Integration:** The agent can call the Calendly API to fetch available meeting slots for the next seven days, providing users with up-to-the-minute information.
* **Modular Booking System:** The final booking confirmation is handled by calling a separate, dedicated n8n workflow. This is an advanced pattern that keeps the main agent clean and promotes reusable components.
* **Persistent Conversation Memory:** Utilizes a PostgreSQL database to store conversation history, allowing the bot to remember context from previous messages for a more natural interaction.
* **Multi-language Support:** The agent is explicitly prompted to detect if the user is writing in Arabic and to respond in Arabic, otherwise defaulting to English.

## 🛠️ Nodes Used

* `Manual Trigger` & `Chat Trigger`: To start the ingestion and chatbot workflows, respectively.
* `Google Drive`: To download the source knowledge document.
* `@n8n/n8n-nodes-langchain.agent`: The central AI agent for the chatbot.
* `@n8n/n8n-nodes-langchain.toolWorkflow`: To call another n8n workflow for the final booking step.
* `n8n-nodes-base.httpRequestTool`: To get real-time availability from the Calendly API.
* `@n8n/n8n-nodes-langchain.vectorStorePinecone`: Used to both write to and read from the knowledge base.
* `@n8n/n8n-nodes-langchain.memoryPostgresChat`: For persistent conversation memory.
* `@n8n/n8n-nodes-langchain.embeddingsOpenAi`: For converting text to vectors.
* `@n8n/n8n-nodes-langchain.lmChatOpenAi`: The language model powering the agent.

## 🔧 Setup & Credentials

To run this solution, you will need to configure the following credentials:

1.  **Google Drive (OAuth2):** For the data ingestion workflow.
2.  **Pinecone API Key:** To connect to the vector database.
3.  **OpenAI API Key:** For embeddings and the main chat model.
4.  **PostgreSQL:** For conversation memory.
5.  **Calendly Access Token (HTTP Header Auth):** For the real-time availability check.

## 📊 Workflow Overview

<img width="1359" height="378" alt="image" src="https://github.com/user-attachments/assets/42e1a24d-7303-4b65-a2d5-1dc5fd96f8c6" />
