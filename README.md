# ⚡ 402 AI Agent Tools: Web Scraper, Search & PDF Reader

Give your AI agents autonomous internet access, bypass anti-bot protections, and extract clean data. 
**Zero subscriptions. Zero credit cards. Pay-per-use via the Lightning Network (L402).**

Autonomous agents often hallucinate or crash because they can't access real-time data, get blocked by Cloudflare, or can't parse complex PDFs. This API acts as a middleware that solves these issues, charging a micro-transaction of just **10 satoshis (~$0.001)** per extraction attempt.

## 🚀 Features

- **🛡️ Anti-Bot Web Scraper:** Bypasses captchas and Cloudflare. Returns clean, structured text (Markdown-ready) perfect for LLM context windows.
- **🔎 Real-Time Web Search:** Performs deep web searches and returns the most relevant, up-to-date snippets using Tavily's AI-optimized engine.
- **📄 PDF Data Extractor:** Reads public PDF URLs and extracts structured text directly from memory.

## 🔌 Quick Integration (OpenAPI)

The easiest way to give your AI agent these capabilities is by importing our OpenAPI schema directly into your framework (LangChain, AutoGPT, Toolhouse, or OpenAI Custom Actions).

**OpenAPI Schema URL:**

https://api-ia-datos.onrender.com/openapi.json

*Your agent will automatically read this file, understand the available tools, and handle the L402 payment flow autonomously.*

## 🛠️ API Endpoints

### 1. Web Scraper (`/api/v1/scrape`)
Extracts clean text from protected URLs.

    curl -i "https://api-ia-datos.onrender.com/api/v1/scrape?url=https://news.ycombinator.com"

### 2. Real-Time Search (`/api/v1/search`)
Searches the web for up-to-date information.

    curl -i "https://api-ia-datos.onrender.com/api/v1/search?query=latest+artificial+intelligence+news"

### 3. PDF Reader (`/api/v1/pdf`)
Extracts text from any public PDF file.

    curl -i "https://api-ia-datos.onrender.com/api/v1/pdf?url=https://bitcoin.org/bitcoin.pdf"

## 💰 How L402 Payments Work

This API strictly implements the **L402 Protocol**. You don't need API keys or monthly subscriptions to start testing.

1. Make a standard `GET` request to any endpoint.
2. Receive a `402 Payment Required` response containing a Lightning Invoice and a Macaroon in the `WWW-Authenticate` header.
3. Your agent pays the invoice (10 sats) via its Lightning node (e.g., Alby Hub).
4. The agent retries the request attaching the `Authorization: L402 <macaroon>:<preimage>` header.
5. The API returns the requested data.

### ⚡ Note on L402 Payment Flow

By design in the L402 protocol, the Lightning invoice must be settled *before* the server releases the final payload. This means the fee applies to the extraction attempt.

**Coming in v1.1 (Roadmap):** 
To prevent agents from paying for failed parses (e.g., if a target website goes offline post-payment), we are implementing a **TTL Grace Period**. If an extraction fails, the agent will be able to reuse the same validated Macaroon to retry the exact same request for a short time window without generating a new invoice. URL caching will also be added to save Lightning routing hops on repeated identical requests.

---
*Built for the Machine Economy.* 🤖⚡
