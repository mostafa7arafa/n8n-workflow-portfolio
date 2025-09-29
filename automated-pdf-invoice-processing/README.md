# Automated PDF Invoice Processing and Notification Pipeline

This n8n workflow creates a fully automated, end-to-end pipeline for processing PDF invoices. The system monitors a Google Drive folder, and upon the upload of a new invoice, it automatically reads the document, extracts key information, logs the data in a Google Sheet, and notifies the billing team via a professionally drafted email.

## 🎯 Goal & Purpose

The primary goal of this workflow is to eliminate the manual, time-consuming, and error-prone task of processing incoming invoices. By automating every step from file detection to data entry and notification, it ensures that invoices are handled quickly, accurately, and consistently.

## ✨ Key Features

* **Event-Driven Automation:** The workflow is initiated by a `Google Drive Trigger` that activates automatically whenever a new file is created in a specific folder.
* **AI-Powered Data Extraction:** A `Google Gemini` model reads the text from the PDF and uses a `LangChain Information Extractor` to pull specific, structured data, including Name, Date, Total Amount, and Type of Transaction.
* **Automated Data Logging:** The extracted information is seamlessly appended as a new row to a designated Google Sheet, creating an organized and real-time ledger of all processed invoices.
* **AI-Generated Email Notifications:** A second, specialized AI (`OpenAI GPT-4.1-mini`) is used to draft a clear and professional notification email for the billing team, summarizing the details of the newly processed invoice.
* **End-to-End Processing:** The workflow manages the entire lifecycle of an incoming invoice, from its arrival in Google Drive to the final confirmation email, requiring no manual intervention.

## 🛠️ Nodes Used

* `Google Drive Trigger`: Watches a specific folder for new files.
* `Google Drive`: Downloads the new invoice file.
* `Extract from File`: Extracts raw text content from the PDF.
* `@n8n/n8n-nodes-langchain.informationExtractor`: The core AI node for structured data extraction.
* `@n8n/n8n-nodes-langchain.lmChatGoogleGemini`: The language model powering the information extractor.
* `Google Sheets`: Appends the extracted data to a spreadsheet.
* `@n8n/n8n-nodes-langchain.openAi`: The model used to generate the notification email.
* `Gmail`: Sends the final notification email.

## 🔧 Setup & Credentials

To run this workflow, you will need to configure the following credentials:

1.  **Google Drive (OAuth2):** For the trigger and file download nodes.
2.  **Google Gemini (PaLM) API Key:** For the information extraction model.
3.  **Google Sheets (OAuth2):** For logging the data.
4.  **OpenAI API Key:** For the email generation model.
5.  **Gmail (OAuth2):** For sending the notification email.

## 📊 Workflow Overview

<img width="1526" height="307" alt="image" src="https://github.com/user-attachments/assets/c6f75f76-bab4-47c6-ade1-dbcc737974bf" />
