# Full-Site Web Scraping with FireCrawl and Asynchronous Polling

This n8n workflow demonstrates how to perform a comprehensive, AI-powered scrape of an entire website using the FireCrawl API. It is designed to handle long-running extraction jobs by implementing an asynchronous polling loop, ensuring the workflow waits patiently until the data is ready before finishing.

## 🎯 Goal & Purpose

The goal is to reliably extract specific, structured data (in this case, quotes and authors) from every page of the target website, `quotes.toscrape.com`. This workflow showcases a robust pattern for interacting with APIs that process jobs in the background, which is common for large-scale data tasks like web scraping.

## ✨ Key Features

* **AI-Powered Extraction:** Leverages FireCrawl to understand a natural language prompt ("*Extract all the quotes and their corresponding authors*") and a defined JSON schema to pull precisely the required data.
* **Full-Site Crawling:** Uses a wildcard in the URL (`https://quotes.toscrape.com/*`) to instruct FireCrawl to find and scrape all pages on the domain, not just the homepage.
* **Guaranteed Data Structure:** By providing a strict JSON schema in the initial request, the workflow guarantees that the final output will be clean, structured, and immediately usable.
* **Asynchronous Job Handling:** The workflow initiates a crawl and then enters a polling loop. It repeatedly checks a status endpoint until the job is complete, making it resilient to long processing times without timing out.

## 🛠️ Nodes Used

* `Manual Trigger`: To start the workflow on command.
* `HTTP Request`: Used twice; first to initiate the FireCrawl job (`POST /v1/extract`) and second to poll for the results (`GET /v2/extract/{jobId}`).
* `If`: Checks if the scraping job is complete by seeing if the returned data is empty.
* `Wait`: Pauses the workflow for a short duration between polling attempts to avoid overwhelming the API.
* `Set`: Cleans up the final output, providing only the extracted data once the job is finished.

## 🔧 Setup & Credentials

To run this workflow, you will need to configure the following:

1.  **FireCrawl API Key:** This should be set up within n8n's HTTP Header Auth credentials and used in both HTTP Request nodes.

## 📊 Workflow Overview

<img width="1412" height="594" alt="image" src="https://github.com/user-attachments/assets/a73d9bc0-6c5a-4308-8c26-63657fc614c4" />
