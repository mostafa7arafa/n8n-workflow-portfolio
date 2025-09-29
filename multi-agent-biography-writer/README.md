# Multi-Agent Biography Generator with Autonomous Revision Loop

This n8n workflow is a sophisticated content generation system that uses a team of three specialized AI agents to autonomously write, evaluate, and refine a creative biography. The workflow ensures a high-quality final output by using an internal revision loop, only saving the result to a Google Doc once it meets a predefined set of standards.

## 🎯 Goal & Purpose

The primary goal is to create a robust content pipeline that goes beyond simple text generation. This workflow mimics a human editorial team: a writer creates the first draft, an editor evaluates it, and a re-writer improves it based on feedback. This process repeats automatically until the content is polished and approved, ensuring a high-quality, well-structured final product.

## ✨ Key Features

* **Multi-Agent AI Team:** The workflow is built around three distinct AI agents, all powered by a single OpenAI model for consistency:
    1.  **Biography Writer:** Creates the initial creative draft in a structured JSON format.
    2.  **Evaluator:** A quality assurance agent that reviews the biography against strict criteria (creativity, structure, engagement, etc.).
    3.  **Optimizer:** A refinement agent that rewrites and enhances the biography based on the Evaluator's feedback.
* **Autonomous Revision Loop:** The core of this workflow. If the `Evaluator` rejects a draft, it's automatically sent to the `Optimizer`. The improved version is then sent back to the `Evaluator` for another review. This loop continues until the biography is approved.
* **Structured Data Handling:** An `Information Extractor` node parses the initial JSON output, ensuring clean and reliable data for the rest of the workflow.
* **Automated Google Docs Integration:** Once the biography is officially approved by the `Evaluator`, the workflow automatically creates a new Google Doc with the correct title and populates it with the final, polished text.

## 🛠️ Nodes Used

* `Chat Trigger`: Allows the workflow to be initiated through a conversational interface.
* `@n8n/n8n-nodes-langchain.agent`: Used to create the three specialized agents (Writer, Evaluator, Optimizer).
* `@n8n/n8n-nodes-langchain.informationExtractor`: To securely parse the JSON output from the first agent.
* `@n8n/n8n-nodes-langchain.lmChatOpenAi`: The single language model powering all AI components.
* `If`: Routes the biography to either the final output or the Optimizer based on the Evaluator's decision.
* `Set`: Functions as a junction to manage the state of the biography as it moves through the revision loop.
* `Google Docs`: Used to create and update the final document.

## 🔧 Setup & Credentials

To run this workflow, you will need to configure the following credentials:

1.  **OpenAI API Key:** For the `OpenAI Chat Model` that powers all agents.
2.  **Google Docs Credentials (OAuth2):** To allow n8n to create and write to Google Docs.

## 📊 Workflow Overview

<img width="1510" height="355" alt="image" src="https://github.com/user-attachments/assets/590f5277-571a-4b88-b78a-f07c3f50a1cc" />
