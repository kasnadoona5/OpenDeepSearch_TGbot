# Telegram AI Deep Search Bot

A Telegram bot that provides AI-powered deep search capabilities by connecting to a custom backend API. This project demonstrates how to use n8n as a secure frontend to handle user management, rate limiting, and communication with a proprietary search service.

**Bot Link:** [https://t.me/your_bot_username](https://t.me/your_bot_username)

---

## Features

-   **AI-Powered Search:** Leverages a custom backend API to perform deep searches and generate intelligent, context-aware answers.
-   **Formatted Responses:** The final answer is sent back to Telegram using HTML parsing for better readability.
-   **User Management & Rate Limiting:** Integrates with Google Sheets to track user interactions and enforce a daily message limit, preventing abuse of the backend service.
-   **Open-Source Frontend:** The complete, sanitized n8n workflow for the bot's frontend is available in this repository.

## How It Works

1.  **User Query:** A user sends a search query to the Telegram bot.
2.  **Rate Limit Check:** The n8n workflow authenticates the user by checking their Telegram ID in a Google Sheet. It verifies their message count for the day, blocking them if the limit is exceeded.
3.  **Secure API Call:** If the user is within their limit, the workflow makes a single, secure HTTP request to a private backend API endpoint. The user's query and all necessary API keys (for services like Serper and OpenRouter, which are managed by the backend) are passed in the request.
4.  **Backend Processing:** The custom backend API receives the query, performs the deep search and AI processing, and returns a final, formatted result.
5.  **Telegram Reply:** n8n receives the result from the backend and sends it directly to the user on Telegram.
6.  **Update Count:** The user's `MessageCount` is incremented in the Google Sheet.

## Setup Instructions

To use this n8n workflow as a frontend for your own service:

1.  **Download:** Download the workflow JSON file from this repository.
2.  **Import:** Import the JSON file into your n8n instance.
3.  **Credentials:** Connect your own credentials for:
    *   Telegram
    *   Google Sheets
4.  **Google Sheet:** Create a new Google Sheet with three columns: `UserID`, `MessageCount`, and `Date`. Update the Google Sheets nodes to point to your new sheet.
5.  **Configure Backend:**
    *   Open the **HTTP Request1** node.
    *   Replace `YOUR_BACKEND_API_ENDPOINT_HERE` with the URL of your own API.
    *   In the "Header Parameters," replace the placeholder values with your actual API keys (`X-API-KEY`, `serper-api-key`, `openrouter-api-key`).
6.  **Activate:** Activate the workflow.

## Tech Stack

-   **Automation Frontend:** [n8n.io](https://n8n.io/)
-   **Backend Service:** Custom API (The logic for this is not included in this repository please check this: https://github.com/kasnadoona5/opnsrchsentient)
-   **External Services:** Serper, OpenRouter (managed via the backend)
-   **Database:** Google Sheets
