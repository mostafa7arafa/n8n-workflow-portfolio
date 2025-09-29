# AI-Powered Customer Support Email Automation

This n8n workflow creates an autonomous AI agent that handles customer support inquiries received via Gmail for the "Al Faysalia Crew Service" company. It intelligently classifies incoming emails, generates context-aware responses using a knowledge base, and replies to the sender automatically.

## 🎯 Goal & Purpose

The primary goal of this workflow is to automate the first line of customer support. It reduces the manual workload on the support team by instantly handling common questions and inquiries, ensuring timely and consistent communication. The system is designed to only engage with relevant support requests, ignoring other types of emails.

## ✨ Key Features

* **Intelligent Email Triage:** Uses a Large Language Model (`Qwen3`) to classify incoming emails into "Customer Support" or "Other" categories, ensuring the agent only acts on relevant queries.
* **Retrieval-Augmented Generation (RAG):** The AI agent is connected to a knowledge base stored in a Pinecone vector store. This allows it to retrieve specific information about company policies and FAQs to answer questions accurately.
* **Autonomous AI Agent:** A dedicated agent (`Deepseek v3.1`) named "Mr. Helpful Arafa" drafts formal, context-aware replies based on the email content and the retrieved knowledge.
* **End-to-End Automation:** The workflow manages the entire process: it's triggered by a new email, generates a response, adds a label to the processed email in Gmail, and sends the reply—all without human intervention.

## 🛠️ Nodes Used

* `Gmail Trigger`: Starts the workflow when a new email is received.
* `@n8n/n8n-nodes-langchain.textClassifier`: Categorizes the email's intent.
* `@n8n/n8n-nodes-langchain.agent`: The core AI agent that processes information and generates text.
* `@n8n/n8n-nodes-langchain.lmChatOpenRouter`: Provides the LLMs (`Qwen3`, `Deepseek v3.1`) for classification and response generation.
* `@n8n/n8n-nodes-langchain.vectorStorePinecone`: Acts as the tool for the agent to retrieve information from the knowledge base.
* `@n8n/n8n-nodes-langchain.embeddingsOpenAi`: Generates embeddings for the RAG process.
* `Gmail`: Used to label the original message and send the reply.
* `NoOp`: A placeholder for emails that are classified as not requiring a response.

## 🔧 Setup & Credentials

To run this workflow, you will need to configure the following credentials and services:

1.  **Gmail Credentials (OAuth2):** To allow n8n to read, label, and reply to emails.
2.  **OpenRouter API Key:** For access to the language models used in the classifier and agent.
3.  **Pinecone API Key:** To connect to the vector database that stores the FAQ knowledge base.
4.  **OpenAI API Key:** For generating the embeddings required by the Pinecone vector store.
5.  **Pinecone Index:** You must have a Pinecone index set up and populated with the FAQ/policy documents for "Al Faysalia Crew Service".


## 📊 Workflow Overview

<img width="1426" height="446" alt="image" src="https://github.com/user-attachments/assets/b72999d1-b5b5-40a2-aa03-3bee15e6580a" />
