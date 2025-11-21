# Building a Voice AI Agent (Telefonist) With n8n & VAPI

## Overview

This document describes how I built a **Voice AI Agent** (a virtual telefonist) that answers phone calls, speaks naturally in Dutch, and creates bookings directly in a business calendar.

The setup uses:

- **VAPI.ai** for real-time telephony, speech-to-text and text-to-speech  
- **A Dutch phone number** connected to VAPI  
- **n8n** as the workflow “brain”  
- **Calendar integration** (e.g. Google Calendar or Outlook) via n8n nodes  

The goal is to handle routine calls — appointment requests, opening hours, basic questions — so employees can focus on work that actually matters, while callers still get a friendly, human-like experience.

---

## 1. System Architecture

The Voice AI Telefonist consists of three main parts.

### 1.1 Voice Interface (VAPI.ai)

VAPI takes care of the entire voice layer:

- answers calls on the Dutch phone number,  
- transcribes the caller’s speech in real time,  
- sends the transcript to n8n,  
- receives text responses from n8n,  
- reads them out loud in a natural Dutch voice.

You can see VAPI as the **ears and mouth** of the agent.

### 1.2 Workflow Logic (n8n)

n8n is the **brain and router**. When VAPI sends a transcript, n8n:

- interprets the question or request,  
- decides whether the caller wants to make a booking or just ask something,  
- asks clarifying questions if needed,  
- interacts with the calendar,  
- sends back the final answer text to VAPI.

Because n8n keeps track of context, the AI can handle gradual conversations like:

> “Ik wil graag een afspraak maken.”  
> “Natuurlijk! Voor welke datum?”  
> “Aanstaande woensdag.”  
> “En welk tijdstip past het beste?”

### 1.3 Calendar Integration

The booking system can use whatever calendar the business prefers, for example:

- **Google Calendar**,  
- **Microsoft Outlook / Office 365**,  
- or a **custom booking API**.

n8n reads available time slots and creates new events when the caller confirms.

---

## 2. Call Flow: From Ring to Booking

A typical call moves through the system as follows:

1. **Caller dials the Dutch number**  
   VAPI answers immediately with a chosen Dutch voice.

2. **VAPI streams transcription to n8n**  
   The caller’s speech is converted to text and posted to n8n (e.g. via webhook).

3. **n8n understands the intent**  
   An AI Agent or LLM node interprets what the caller wants and keeps a short memory of previous turns.

4. **Booking logic (if needed)**  
   If the caller wants an appointment, n8n:
   - checks availability in the calendar,  
   - proposes one or more time slots,  
   - asks for confirmation.

5. **n8n sends response text back to VAPI**  
   VAPI does TTS (Text-to-Speech), for example:

   > “Ik heb woensdag om 14:00 een plekje vrij. Zal ik dat voor u inplannen?”

6. **Caller confirms**  
   For example: “Ja, graag.”

7. **n8n creates the calendar event**  
   An event is created in the chosen calendar with date, time and optional notes.

8. **VAPI ends the call**  
   The agent confirms the booking, says goodbye and hangs up.

Because everything runs in real time, the experience is close to talking to a human receptionist.

---

## 3. n8n Workflow Structure

Inside n8n, the workflow is split into a few logical modules.

### 3.1 Webhook / Call Event Node

This entry node receives:

- the caller transcript,  
- caller ID,  
- call/session ID,  
- language and timestamp metadata.

It normalises the data so the rest of the flow can work with a consistent structure.

### 3.2 AI Agent Node

The AI Agent node is responsible for:

- understanding natural language,  
- deciding on the next action (answer, ask a question, check calendar, etc.),  
- generating short, polite Dutch responses.

For cost-efficiency the models are used like this:

- **GPT-4o-mini** for ~90% of all turns (cheap and fast),  
- **GPT-4.1** or **Claude Sonnet** only for edge cases or more complex reasoning.

### 3.3 Decision Logic

Simple function nodes or IF nodes decide:

- Is this about opening hours or location info?  
- Is this about pricing or general info?  
- Is this a booking or rescheduling request?  
- Does the caller need a reminder or confirmation SMS (future feature)?

### 3.4 Calendar Nodes

Calendar nodes handle:

- free/busy lookups,  
- creating events,  
- formatting date/time in a way that is readable for the caller.

### 3.5 Response Node & Memory

Finally:

- a Response node sends the reply text back to VAPI,  
- a small Memory mechanism keeps useful context (desired date, name, service type), so the AI doesn’t ask the same question twice.

---

## 4. Voice Quality, Tone and Prompting

To make the telefonist sound professional and genuinely Dutch, the system prompt includes instructions like:

- be polite and calm,  
- keep answers short and clear,  
- avoid slang and unnecessary small talk,  
- always confirm the booking details,  
- use simple language so everyone understands.

A typical system prompt could be:

> “Je bent een vriendelijke en professionele Nederlandse telefoniste.  
> Je helpt mensen met het inplannen van afspraken en het beantwoorden van eenvoudige vragen.  
> Houd je antwoorden kort, duidelijk en beleefd.”

This keeps the brand voice consistent, no matter who calls or when they call.

---

## 5. Latency and Model Choice

For voice, **latency is critical**. If the AI waits too long before responding, the call feels robotic or like a bad connection.

In practice we aim for:

- **Ideal latency per turn:** ~300–800 ms  
- **Maximum acceptable:** ~1–1.5 seconds  

To stay within this range we:

- use **small, optimised models** (like GPT-4o-mini or Gemini Flash) for most turns,  
- enable **streaming** wherever possible (STT, LLM, TTS),  
- keep prompts and replies short so there are fewer tokens to process.

### 5.1 Model Comparison (Official Public Pricing)

The table below compares several models that could be used in this voice workflow.

| Model                  | Role in Voice Agent                        | Input Cost (≈1M tokens) | Output Cost (≈1M tokens) | Notes                                       |
|------------------------|---------------------------------------------|--------------------------|---------------------------|---------------------------------------------|
| **GPT-4o-mini**        | Default for understanding & replies         | ~$0.15                   | ~$0.60                    | Very cheap, fast, ideal default model       |
| **GPT-4.1**            | Complex reasoning / tricky calls            | ~$2.00                   | ~$8.00                    | Smarter, used sparingly                     |
| **ChatGPT-5**          | Premium, high-end reasoning                 | ~\$1.25                  | ~\$10.00                  | Strong reasoning, more expensive per token  |
| **Claude 3.5 Sonnet**  | Natural chat, polite call handling          | ~$3.00                   | ~$15.00                   | Great conversational quality                |
| **Gemini 2.0 Flash**   | Very cheap high-volume option               | ~\$0.10                  | ~\$0.40                   | Extremely cost-effective                    |
| **Grok 2**             | Simple calls, high throughput               | ~$2.00                   | ~$10.00                   | Alternative for larger deployments          |

For this telefonist, a realistic setup is:

- use **GPT-4o-mini** or **Gemini Flash** for almost everything,  
- escalate rarely to **GPT-4.1**, **Claude** or **ChatGPT-5** when you really need better reasoning.

---

## 6. Cost of the Voice AI Telefonist

To get a feeling for the costs, we can estimate a typical call.

Assumptions:

- Average call: **3 minutes**  
- Around **12 turns** (caller + AI back-and-forth)  
- Per turn:
  - ±50 tokens from the caller after transcription  
  - ±150 tokens in the AI reply  

Total per call:

- Input: about **600 tokens**  
- Output: about **1,800 tokens**

### 6.1 Example: GPT-4o-mini

Using the prices above:

- Input (600 tokens): ~0.0006M × $0.15 ≈ **$0.00009**  
- Output (1,800 tokens): ~0.0018M × $0.60 ≈ **$0.00108**  

**Total LLM cost per 3-minute call ≈ $0.00117**  
→ roughly **0.12 dollar-cent per call**.

For **1,000 calls per month**:

- 1,000 × $0.00117 ≈ **$1.17 per month** in LLM costs.

Even if we include a bit of overhead or occasionally use a more expensive model, the model costs remain **very low**.  
Most of the total cost will come from telephony minutes, STT and TTS usage, not from the language model itself.

---

## 7. Why a Voice AI Telefonist Is Useful

For a business, this setup brings several clear advantages:

- **Never miss a call** – the AI picks up 24/7.  
- **Automatic bookings** – appointments go straight into the calendar.  
- **Consistent politeness** – no stress, no tired employees, always friendly.  
- **Lower costs** – especially for evenings, weekends and peak hours.  
- **Scales easily** – 1, 5 or 20 parallel calls are no problem.

---

## 8. Future Improvements

Possible extensions:

- CRM lookups (“Heeft u een klantnummer voor mij?”)  
- Sending confirmation or reminder SMS/WhatsApp messages  
- Sending payment links after certain bookings  
- Deeper integration with custom ticketing or back-office systems  
- Using a premium model (e.g. GPT-5 or Claude) for specific high-value clients

---

## Conclusion

By combining **VAPI** for real-time telephony, **n8n** for workflow logic and modern LLMs for language understanding, it is possible to build a Dutch Voice AI telefonist that:

- answers calls,  
- understands what people want,  
- books appointments directly in the calendar,  
- and does all of this with low latency and very low model costs.

The result is an always-available, professional receptionist that scales with the business and forms a strong base for more advanced customer service automation in the future.