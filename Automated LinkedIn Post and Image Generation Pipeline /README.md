# Automated LinkedIn Post and Image Generation Pipeline

This n8n workflow automates the entire creative process for generating a LinkedIn post, including both the written content and a custom-tailored companion image. The system uses a sophisticated dual-agent AI architecture to handle distinct tasks: one agent for content writing and another for visual prompt engineering.

## 🎯 Goal & Purpose

The goal is to streamline social media content creation by transforming a simple topic and target audience into a complete, ready-to-publish post. By separating the writing and visual creation tasks between two specialized AI agents, the workflow ensures higher quality and more relevant output for both the text and the image.

## ✨ Key Features

* **Dual-Agent AI System:** Employs two distinct AI agents working in sequence:
    1.  A **Content Creator** (`Google Gemini`) researches and writes an engaging LinkedIn caption.
    2.  A **Visual Prompt Engineer** (`OpenAI GPT-4o`) analyzes the caption and target audience to craft a detailed, cinematic prompt for an image generator.
* **Real-Time Web Research:** The Content Creator agent is equipped with a `Tavily` search tool, allowing it to access up-to-date information to create timely and accurate posts.
* **AI-Powered Art Direction:** Instead of using simple keywords, a dedicated agent creates a rich, descriptive prompt designed to produce a professional and thematically appropriate image from DALL-E.
* **End-to-End Automation:** The entire process, from a user filling out a form to receiving a finished post with an image attachment, is fully automated.
* **Form-Based Trigger:** Kicks off the entire pipeline with a simple form, making it incredibly easy for a user to input their content requirements (Topic, Target Audience, and delivery Email).

## 🛠️ Nodes Used

* `Form Trigger`: A manual trigger that collects user input for the post.
* `@n8n/n8n-nodes-langchain.agent`: Used twice for the **Content creator** and **Write Image Prompt** agents.
* `@n8n/n8n-nodes-langchain.lmChatGoogleGemini`: Powers the content creation agent.
* `@n8n/n8n-nodes-langchain.lmChatOpenAi`: Powers the visual prompt engineering agent.
* `@tavily/n8n-nodes-tavily.tavilyTool`: Provides real-time web search capabilities.
* `HTTP Request`: Makes a direct API call to the OpenAI DALL-E service to generate the image.
* `Convert to File`: Converts the Base64 image data from the API into a binary file for attachments.
* `Gmail`: Sends the final text and image as an email (used for testing in place of a direct LinkedIn post).

## 🔧 Setup & Credentials

To run this workflow, you will need to configure the following credentials:

1.  **Google Gemini (PaLM) API Key:** For the content creator agent.
2.  **Tavily API Key:** For the web search tool.
3.  **OpenAI API Key:** Used for both the visual prompt agent and for authenticating the DALL-E HTTP request.
4.  **Gmail Credentials (OAuth2):** For sending the final email with the attachment.

## 📊 Workflow Overview
<img width="1502" height="427" alt="image" src="https://github.com/user-attachments/assets/e27b4d3b-d86e-40d4-9a42-7189e2f946a8" />
