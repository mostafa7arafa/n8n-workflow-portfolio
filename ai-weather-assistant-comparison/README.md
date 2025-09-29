# AI Weather Assistant: A Comparison of Two n8n Architectures

This n8n canvas contains two distinct and independent workflows that both function as an AI-powered weather assistant. The purpose is to showcase and compare two different design patterns for building AI applications: a modern, self-contained **AI Agent** versus a traditional, explicit **AI Workflow (Pipeline)**.

## 🎯 Goal & Purpose

The goal is to create a conversational AI that can provide the current weather for a city specified by the user. By building this assistant in two different ways, this project highlights the trade-offs and advantages of each architectural approach.

---

### Workflow 1: The Self-Contained AI Agent

This approach uses a single, intelligent AI agent that is given a goal and a tool. The agent itself is responsible for understanding the user's request, extracting the necessary information (the city), deciding to use the tool, and formatting the final response.

<img width="795" height="633" alt="image" src="https://github.com/user-attachments/assets/e15b629b-6391-4bfa-bc44-df95b8e2406f" />
 
 **Key Features:**
* **Simplicity & Elegance:** The entire logic is encapsulated within a single `LangChain Agent` node.
* **Tool-Based Functionality:** The agent is equipped with a `get_weather` tool, which it learns to call when a user asks about the weather.
* **Autonomous Operation:** The AI handles the entire process from intent recognition to execution, making the workflow very concise.

---

### Workflow 2: The Explicit AI Workflow (Pipeline)

This approach uses a more traditional, step-by-step pipeline where each node has a single, well-defined responsibility. The data flows through a chain of classification, extraction, data fetching, and final formatting.

<img width="1463" height="471" alt="image" src="https://github.com/user-attachments/assets/d6858132-976d-4304-a990-99396457fd3e" />
 
**Key Features:**
* **Granular Control:** Each step of the process is explicit and isolated, making it easy to debug or modify individual components.
* **Step-by-Step Logic:** The flow is easy to follow:
    1.  **Classify:** A `Text Classifier` first determines if the request is about weather.
    2.  **Extract:** An `City Extractor` pulls out the city name.
    3.  **Fetch:** A standard `Get Wheather` node gets the data from the API.
    4.  **Format:** A final `LangChain Agent` formats the raw data into a friendly message.
* **Predictability:** The workflow's path is rigidly defined, offering a high degree of predictability and control over the process.

## 🛠️ Nodes Used

Both workflows utilize a combination of the following nodes:

* `Chat Trigger`: To receive user input conversationally.
* `@n8n/n8n-nodes-langchain.agent`: The core AI brain for both approaches.
* `@n8n/n8n-nodes-langchain.textClassifier`: Used in the pipeline approach for intent recognition.
* `@n8n/n8n-nodes-langchain.informationExtractor`: Used in the pipeline approach for entity extraction.
* `@n8n/n8n-nodes-langchain.lmChatGoogleGemini`: The language model powering all AI components.
* `HTTP Request` & `HTTPRequest Tool`: To connect to the OpenWeatherMap API.

## 🔧 Setup & Credentials

To run these workflows, you will need to configure the following:

1.  **Google Gemini (PaLM) API Key:** Required for all AI nodes.
2.  **OpenWeatherMap API Key:** Required for the `HTTP Request` and `HTTPRequest Tool` nodes to fetch weather data.

## 📊 Workflow Overview

<img width="1597" height="382" alt="image" src="https://github.com/user-attachments/assets/51060869-f1fd-4afe-a20c-78d6f29a7d52" />
