# Telegram AI Chatbot with Human-in-the-Loop (HITL) Approval

This advanced n8n workflow deploys a conversational AI assistant, "Mostafios," on Telegram to handle customer support for Al Faysalia Crew Service. The key feature of this workflow is a robust **Human-in-the-Loop (HITL)** mechanism, which ensures that no AI-generated message is sent to a customer without prior review and approval from a human supervisor.

## 🎯 Goal & Purpose

The purpose of this workflow is to create a reliable and quality-controlled customer support chatbot. While the AI handles the initial response generation using a knowledge base, the HITL system provides a critical safety layer. This prevents errors, ensures brand voice consistency, and allows for continuous improvement of the AI's responses through guided feedback.

## ✨ Key Features

* **Conversational AI Assistant:** An AI agent (`OpenAI`) named "Mostafios" engages with users on Telegram, maintaining conversation history using built-in memory.
* **Knowledge Base Integration (RAG):** The agent answers questions accurately by retrieving information from a company FAQ stored in a Pinecone vector database.
* **Human-in-the-Loop (HITL) Verification:** Before any message is sent to the customer, it is first sent to a human supervisor for approval. The workflow pauses until the supervisor responds.
* **Iterative Feedback & Optimization:** If the supervisor is not satisfied with the AI's answer, they can provide natural language feedback (e.g., "make it more formal"). This feedback is sent to a secondary AI "Optimizer" (`Google Gemini`) which refines the original message.
* **AI-Powered Approval Check:** The supervisor's response is intelligently classified by a `Google Gemini` model to determine if it's an approval or a request for modification, seamlessly directing the workflow's next steps.

## 🛠️ Nodes Used

* `Telegram Trigger`: Initiates the workflow upon receiving a new message.
* `If`: Filters out initial `/start` messages.
* `@n8n/n8n-nodes-langchain.agent`: Used for two distinct roles: the primary **Customer Support** agent and the secondary **Optimizer** agent.
* `@n8n/n8n-nodes-langchain.memoryBufferWindow`: Provides conversational memory to the primary agent.
* `@n8n/n8n-nodes-langchain.vectorStorePinecone`: The knowledge base tool (RAG).
* `@n8n/n8n-nodes-langchain.embeddingsOpenAi`: Generates embeddings for the RAG process.
* `@n8n/n8n-nodes-langchain.lmChatOpenAi`: Powers the primary customer support agent.
* `@n8n/n8n-nodes-langchain.lmChatGoogleGemini`: Powers the Optimizer and the Approval Check classifier.
* `@n8n/n8n-nodes-langchain.textClassifier`: Determines if a supervisor's response is an approval or denial.
* `Telegram`: Used to send the final message to the customer and to manage the HITL feedback loop with the supervisor.

## 🔧 Setup & Credentials

To run this workflow, you will need to configure the following:

1.  **Telegram API Credentials:** To connect your bot.
2.  **Pinecone API Key:** For the knowledge base connection.
3.  **OpenAI API Key:** For the primary agent's LLM and for embeddings.
4.  **Google Gemini (PaLM) API Key:** For the Optimizer and Approval Check models.
5.  **Supervisor Chat ID:** You must manually set the supervisor's Telegram Chat ID in the "Feedback" Telegram node to ensure approval requests are sent to the correct person.

**IMPORTANT:** Never commit your secret keys or credentials directly to your GitHub repository.

## 📊 Workflow Overview

<img width="1465" height="456" alt="image" src="https://github.com/user-attachments/assets/d31642eb-aca3-4193-8095-f52441bbb7d1" />
