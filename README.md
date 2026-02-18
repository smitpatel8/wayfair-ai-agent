# Wayfair Market Trend Discovery Agent 🚀

**An automated, AI-powered market intelligence agent designed to generate actionable business insights for the Home Decor giant Wayfair.**

![Project Banner](https://via.placeholder.com/1000x300?text=Wayfair+Market+Trend+Discovery+Agent)

## 📖 Overview

The **Wayfair Market Trend Discovery Agent** is a complex orchestration workflow powered by **n8n** and **Google Gemini**. It automates the traditionally manual process of market research by gathering, analyzing, and reporting on rug trends.

Unlike standard trend tools that focus on aesthetic "buzz," this agent was engineered to identify **commercial viability**, inventory gaps, and pricing opportunities. The system ingests real-time data from competitors, design blogs, and search trends, processing it through specialized AI personas to output a structured HTML report for stakeholders.

## 🎯 Project Goal

To transform raw, unstructured market data into a clear, strategic roadmap for Wayfair's inventory planning and buying teams. The ultimate goal was to move beyond *aesthetic* forecasting and answer the critical business question: **"What should we stock next, and at what price?"**

---

## 🏗️ System Architecture & Workflows

The project is built on **n8n** for orchestration and **Google Gemini** for cognitive processing. It consists of several interconnected workflows that handle specific tasks in the data pipeline.

### 1. The Master Orchestrator (`market_trend_workflow.json`)
This is the brain of the operation.
* **Function:** Handles incoming chat messages and determines "User Intent" (e.g., is the user asking for a trend report, specific competitor data, or a deep dive?).
* **Logic:** Uses an IF switch to route the request to the appropriate sub-workflow (RSS fetching, Google Search, or Competitor Scraping).

### 2. Data Ingestion Layer
The agent pulls data from three primary sources to build a holistic market view:

* **Competitor Intelligence (`competitor_monitoring_workflow.json`):**
    * **Targets:** Scrapes product data (price, material, patterns) from **Amazon**, **Walmart**, and **Wayfair**.
    * **Deep Dive:** Includes a specialized sub-routine (`amazon_scrapper_workflow.json`) to extract deep product details, collections, and "Best Seller" signals from Amazon.
    * **Output:** benchmarks Wayfair's current catalog against competitor moves.

* **Trend Monitoring (`rss_workflow.json`):**
    * **Sources:** Monitors industry blogs and design feeds (e.g., Obeetee, Sisal, Locust).
    * **Filter:** Automatically filters for "Recent Items" to ensure reports only contain fresh signals.

* **Search Validation (`Google Search_workflow.json`):**
    * **Function:** Dynamically fetches fresh web results to validate search volume and user intent.
    * **Goal:** Confirms if a "trend" is actually being searched for by real users.

### 3. Cognitive Processing & Reporting (`final_workflow_n8n.png`)
* **Aggregation:** Merges data from all sources (RSS, Scrapers, Search) into a single JSON object.
* **AI Analysis (Gemini):** The core intelligence engine. It utilizes specific "System Messages" to analyze the data stream. It filters noise (non-rug items), identifies patterns (e.g., "Washable," "Jute"), and synthesizes insights.
* **HTML Generation:** The agent autonomously writes a self-contained HTML trend report with CSS styling, ready for download.

---

## 🧪 The "Persona" Experiment (A/B Testing)

A key innovation of this project was testing **5 distinct AI Personas** to determine which System Message yielded the most business value. The goal was to see how the *same data* could result in different insights depending on the AI's "role".

| Variation | Persona | Focus | Outcome |
| :--- | :--- | :--- | :--- |
| **V1** | **Commercial Buyer** | Sales volume, inventory gaps, pricing. | **🏆 WINNER:** Provided the most actionable data (e.g., "Stock geometric patterns in the $50 range"). |
| **V2** | **Aesthetic Director** | Visuals, mood, styling. | Good for marketing, but lacked hard data for inventory planning. |
| **V3** | **Competitor Scout** | Specific retailer moves (Target vs. Amazon). | Useful for pricing strategy, but too narrow for general trends. |
| **V4** | **Pain-Point Researcher** | Functionality (Washable, Pet-friendly). | Good for R&D/Product Development, less for immediate buying. |
| **V5** | **Executive Strategist** | High-level "80/20" overview. | Too brief; missed critical nuance required for decision making. |

### 💡 Key Insight
The **Commercial Buyer** persona was superior because it bridged the gap between abstract trends and concrete SKU planning. It translated "cool designs" into **Attributes Tables** containing:
* **Size:** Volume drivers (e.g., 5x8, Runners).
* **Price:** Specific "Sweet Spot" ranges (e.g., $50-$150).

---

## 📄 Sample Output

The agent produces a professional **"Rugs Category Trend Report"** containing:

1.  **Executive Summary:** High-level market movements (e.g., "Shift toward Washable Traditionals").
2.  **Trend Deep-Dives:** Detailed breakdown of top 3 trends with attribute tables.
3.  **Attribute Analysis:**
    * *Size:* $2\times3$, $5\times7$, $8\times10$.
    * *Color:* Grey, Cream, Earthy tones.
    * *Price:* $50 to $500.
4.  **Source Citation:** All insights are backed by dated sources (Last 7 Days).

---

## 🛠️ Technology Stack

* **Orchestration:** [n8n](https://n8n.io/)
* **AI Model:** Google Gemini (via API)
* **Scripting:** JavaScript (for data parsing and normalization)
* **Output:** HTML5/CSS3

## 🚀 Getting Started

1.  **Prerequisites:** n8n instance (Self-hosted or Cloud), Google Gemini API Key.
2.  **Import Workflows:** Import the `.json` workflow files into your n8n editor.
3.  **Configure Credentials:** Add your Google Gemini API key in the credentials section.
4.  **Run:** Execute the `Market Trend Discovery Agent` workflow and prompt it (e.g., *"Show me trending rugs for this month"*).

---
*Built by Smit Patel*
