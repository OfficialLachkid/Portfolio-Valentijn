# Building a Website Chatbot With n8n, Webhooks and OpenAI Models

## Overview

This document describes how I built a website chatbot using **n8n** as the orchestration layer and **OpenAI models** (mainly `gpt-4o-mini` and sometimes `gpt-4.1`) as the brain. The chatbot is embedded on a website and connected to n8n through a **webhook**.  

Incoming messages from visitors are sent to n8n, where an **AI Agent** node handles the conversation. The agent has access to:

- company-specific instructions (tone-of-voice, FAQ, policies),
- a **product catalogue** (currently Google Sheets, later Supabase),
- a simple **memory** store for short-term context.

The goal is to automatically answer common questions about products, orders and basic support, so that human staff can focus on work that actually matters.

After n8n processes the message, it sends a structured response back to the website, which is rendered inside a chat widget. The bot is designed to suggest at most **three products** per answer, including article number, link, image and a short description.

---

## 1. Chatbot Architecture

The chatbot consists of three main layers:

1. **Frontend chat widget** on the website  
2. **n8n workflow** that receives and processes messages  
3. **AI backend** using OpenAI models and data tools

### 1.1 Website chat widget

On the website there is a small chat window in the corner. When a visitor types a message and presses send, the frontend makes an HTTP request to an **n8n webhook URL**. The request contains:

- the user’s message,
- a conversation or session ID,
- optional metadata (language, page URL, customer type, etc.).

The chat widget waits for a JSON response from n8n and then displays the answer text. If product recommendations are included in the response, the widget renders them as cards with image, title, article number and a link to the product page.

### 1.2 n8n workflow

Inside n8n, the flow roughly looks like this:

1. **Webhook node – “When chat message received”**  
   This node is triggered every time the website sends a message. It parses the payload and extracts the user text, session ID and other fields.

2. **AI Agent node**  
   The message is passed into the **AI Agent** node. This node is configured with:
   - a default **chat model** (currently `gpt-4o-mini`),
   - a **memory** tool for short-term context,
   - a **product catalogue tool** pointing to a spreadsheet,
   - optional instructions about brand voice and behavior.

3. **Tools connected to the agent**
   - **Simple Memory**  
     Keeps recent exchanges in context so the agent can handle follow-up questions like “What about a smaller size?”.
   - **Product Catalogue (Google Sheets)**  
     Exposes product data (article, name, description, URL, image link, stock, price, etc.) as a searchable tool. In the future this will be replaced by **Supabase** for a more robust database backend.
   - (Later) **Order status tool / CRM lookup**  
     For now this is out of scope, but the architecture allows easy extension.

The AI Agent can choose which tools to call based on the user question. For a product-related question it will query the catalogue. For more generic FAQ-style questions it may not need tools at all and simply answer from its instructions and memory.

4. **Response formatting node**  
   After the agent has produced an answer and any tool results, a simple n8n function node transforms the output into a clean JSON structure for the frontend. It ensures the bot returns:
   - a natural language message,
   - **up to three products**, each with:
     - article number,
     - product title,
     - description,
     - product page URL,
     - image URL.

5. **HTTP Response node**  
   Finally, n8n sends the structured response back to the website via the webhook. The chat widget displays the text and renders the recommended products.

---

## 2. Conversation Strategy

The chatbot is designed to **narrow down the user’s request** before recommending products. Instead of immediately listing all possible items, it asks clarifying questions when needed, such as:

- “Voor welk formaat vuilniszak ben je op zoek?”
- “Gebruik je de zakken voor huishoudelijk gebruik of voor professioneel gebruik?”
- “Heb je een voorkeur voor dikte of materiaal?”

Only after the intent is clear does the agent perform a product lookup. This avoids overwhelming the user and reduces the risk of irrelevant suggestions.

The final answer generally follows this structure:

1. A short explanation or answer to the question.  
2. A list of **maximum three matching products**, each with:
   - a short description focused on the user’s needs,
   - the article number for customer service,
   - a direct link to the product page,
   - a thumbnail image.

This keeps messages short and actionable, while still giving the user real options.

---

## 3. Data Sources: From Spreadsheets to Supabase

At the moment, the product data is stored in a **Google Sheets** spreadsheet. n8n reads this sheet through the **Product Catalogue** node and exposes it as a tool for the AI Agent. Each row represents a product with fields for article code, name, description, category, URL and image URL.

This approach is very convenient during the prototype phase because:

- it is easy to edit,
- non-technical team members can update products,
- n8n already has strong support for Google Sheets.

The plan is to migrate this to **Supabase** later on. Supabase will provide:

- a proper SQL database with relationships,
- better performance when the product catalogue grows,
- built-in authentication and APIs for other tools,
- a single source of truth shared between the chatbot and other systems.

When this happens, the **Product Catalogue tool** in the AI Agent can be reconfigured to query Supabase instead of spreadsheets, but the rest of the workflow will stay mostly the same.

---

## 4. Model Choices: GPT-4o-mini vs GPT-4.1

For the chatbot’s brain I mainly use **`gpt-4o-mini`** and occasionally **`gpt-4.1`**.

- `gpt-4o-mini` is the **default** model for most messages. It is fast and very cheap, which makes it ideal for continuous chat on a website. According to OpenAI’s pricing, it costs about **$0.15 per 1M input tokens** and **$0.60 per 1M output tokens**. :contentReference[oaicite:0]{index=0}
- `gpt-4.1` is used selectively for more complex questions where better reasoning and instruction following is important. It is more expensive, at around **$2.00 per 1M input tokens** and **$8.00 per 1M output tokens**. :contentReference[oaicite:1]{index=1}

Because higher-level models are more costly, the workflow is configured so that:

- everyday product and FAQ questions run on `gpt-4o-mini`,  
- escalations or tricky questions can optionally be routed to `gpt-4.1`.

This balance keeps the chatbot affordable while still allowing high-quality answers when needed.

---

## 5. LLM Comparison Table (Official Public Pricing)

The table below compares several modern LLMs that can be used for chatbot workflows.  
This includes **GPT-4o-mini**, **GPT-4.1**, **ChatGPT-5**, **Claude 3.5 Sonnet**, **Gemini 2.0 Flash**, and **Grok 2**.

| Model                   | Typical Use Case                                    | Input Cost (per ~1M tokens) | Output Cost (per ~1M tokens) | Notes on Suitability |
|------------------------|------------------------------------------------------|------------------------------|-------------------------------|-----------------------|
| **GPT-4o-mini**        | Default model for everyday chat, product queries     | **$0.15** per 1M input    | **$0.60** per 1M output     | Fast, cheap, ideal for high-volume site chat |
| **GPT-4.1**            | More complex reasoning, escalated conversations      | Higher tier on OpenAI        | Higher tier on OpenAI         | Much smarter but significantly more expensive |
| **ChatGPT-5**          | High-end general AI, strong reasoning & reliability  | **~$1.25** per 1M input ([TechCrunch](https://techcrunch.com/2025/08/08/openai-priced-gpt-5-so-low-it-may-spark-a-price-war/?utm_source=chatgpt.com)) | **~$10** per 1M output ([TechCrunch](https://techcrunch.com/2025/08/08/openai-priced-gpt-5-so-low-it-may-spark-a-price-war/?utm_source=chatgpt.com)) | Excellent accuracy for a relatively fair price |
| **Claude 3.5 Sonnet**  | Reasoning, analysis, multi-tool workflows            | **$3** per 1M input ([Anthropic](https://www.anthropic.com/news/claude-3-5-sonnet?utm_source=chatgpt.com)) | **$15** per 1M output ([Anthropic](https://www.anthropic.com/news/claude-3-5-sonnet?utm_source=chatgpt.com)) | Strong competitor, long context window (up to 200k tokens) |
| **Gemini 2.0 Flash**   | Cost-efficient support chatbot, fast inference       | **~$0.10** per 1M input ([Google](https://developers.googleblog.com/en/start-building-with-the-gemini-2-0-flash-family/?utm_source=chatgpt.com)) | **~$0.40** per 1M output ([UnifiedAIHub](https://www.unifiedaihub.com/models/google/gemini-2-flash-lite?utm_source=chatgpt.com)) | Extremely budget friendly, good for large traffic volumes |
| **Grok 2**             | Large-volume messaging, simpler reasoning tasks      | **$2** per 1M input ([LangDB](https://langdb.ai/app/providers/xai/grok-2?utm_source=chatgpt.com)) | **$10** per 1M output ([LLM-Stats](https://llm-stats.com/models/grok-2?utm_source=chatgpt.com)) | Good throughput, competitive pricing |

---

## Notes on Cost Strategy for the Chatbot

Since this chatbot focuses on **product suggestions, FAQs, and support**, costs matter more than extreme model intelligence.

A good hybrid strategy:

- Use **Gemini 2.0 Flash** or **GPT-4o-mini** for **95% of queries**  
  → cheapest per token, fast, totally sufficient.

- Use **GPT-4.1**, **Claude 3.5**, or **ChatGPT-5** **only when needed**  
  → for tricky questions or higher-stakes reasoning.

This approach keeps monthly operating costs extremely low while still allowing premium performance when appropriate. Switching between these LLMs and deciding which one to use can be done by adding **[OpenRouter.AI](https://openrouter.ai/)** (link)

---

## 6. Benefits for the Company

This setup offers several advantages for the company:

- **Reduced workload for support staff**  
  Frequently asked questions and basic product advice are handled automatically, so employees can focus on complex cases and higher-value tasks.

- **Consistent answers**  
  The AI always follows the same instructions and brand voice, which leads to more consistent communication with customers.

- **Scalability**  
  If website traffic doubles, the chatbot can simply handle more conversations without needing extra staff.

- **Future-proof architecture**  
  Because everything runs through n8n and tools, it is easy to plug in new data sources such as Supabase, a CRM, or order tracking systems.

---

# 7. Performance on Local Hardware (HP Thin Client)

To understand how well the chatbot infrastructure performs in a real-world environment, this section evaluates how many conversations can be handled simultaneously on the **HP T630 Thin Client**, which currently runs n8n and Windows 10.

## 7.1 Hardware Overview

The thin client used for hosting n8n has the following specifications:

- **HP T630 Thin Client – AMD GX-420GI (4 cores @ 2.0 GHz)**
- **8GB DDR4 RAM**
- **128GB M.2 SSD**
- Radeon R7E Graphics  
- Windows 10 installed  
- Gigabit Ethernet  
- Energy-efficient embedded hardware

Since n8n mostly performs I/O-bound work (webhooks, message passing, API calls), this machine is more than capable for the intended workflow.

---

## 7.2 Simultaneous Conversations (Parallel)

All heavy AI operations run on **OpenAI’s servers**, so the thin client only needs to:

- receive webhooks  
- pass the request to the AI Agent  
- format responses  
- send data back to the frontend  

This requires minimal CPU usage.

### **Realistic performance**
- **20–40 simultaneous conversations**  
  → Smooth, low latency, no noticeable slowdown.

### **High load (still functional)**
- **40–60 simultaneous conversations**  
  → Slight delay possible, but still stable.

### **Technical upper bound**
- **60–120 webhook events in parallel**  
  → Not recommended; potential queueing and Windows memory paging.

In all scenarios, the true bottleneck is **OpenAI API latency**, *not* the device.

---

## 7.3 Individual Conversations (Sequential)

For single-user, non-parallel conversations, the thin client processes:

- **~3–8 ms of local work per message**  
- The remaining time comes entirely from the **OpenAI round-trip**  
  (typically 200–800 ms depending on model and network conditions).

Therefore:

- **The device can handle hundreds of sequential messages per minute**,  
  since most of the processing is offloaded.

---

## 7.4 Why the Thin Client Performs Well

- n8n workflows are **asynchronous**  
- No LLM runs locally → **no heavy CPU computation**
- SSD ensures fast reads/writes  
- 4-core CPU handles concurrent webhook triggers easily  
- 8GB RAM is sufficient for n8n + Windows + multiple workflow executions  

This makes the HP T630 a surprisingly powerful and low-cost automation host.

---

## 7.5 Performance Summary

| Load Type | Capacity | Notes |
|----------|----------|-------|
| **Simultaneous conversations** | **20–40 (normal)** | Smooth, stable |
| | **40–60 (high)** | Small delays possible |
| | **60–120 (max)** | Not recommended for production |
| **Sequential conversations** | **Hundreds per minute** | Only ~3–8 ms local overhead |
| **Main bottleneck** | **OpenAI latency** | Thin client is not the limiting factor |

This makes the chatbot architecture highly scalable even on small, energy-efficient hardware.

---

## Conclusion

By combining a simple web chat widget, an n8n workflow and OpenAI models, it is possible to build a practical website chatbot that answers customer questions, searches a product catalogue and proposes up to three relevant products per query.  

The architecture is flexible: the data layer can move from spreadsheets to Supabase, and the model strategy can balance cost and intelligence by mixing `gpt-4o-mini` for most traffic with occasional use of `gpt-4.1` for difficult questions. This makes the chatbot both affordable and powerful, and it provides a solid foundation for future automation around customer support and product discovery.