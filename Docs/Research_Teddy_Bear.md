# Teddy – AI-Generated Social Interaction Tasks using n8n

## Overview

In this project we created an AI-powered system for **Teddy**, a teddy bear that is passed from person to person.  
Whenever someone receives Teddy, they scan a **QR code** attached to the bear.  
This QR code leads them to a small website where they receive a **social-interaction task**, such as:

> “Vraag iemand hoe zijn dag was.”  
> “Zeg hallo tegen iemand die je nog nooit hebt gesproken.”  
> “Geef iemand een compliment.”

These tasks are meant to gently stimulate positive social behavior, short conversations, and human connection in a simple and playful way.

Tasks are **automatically generated**, stored, and refreshed through an **n8n workflow** that uses AI to produce new, unique prompts.

---

## 1. How the System Works

The Teddy system consists of three components:

1. **A QR code** attached to the teddy bear  
2. **A small website** that displays a task when opened  
3. **An n8n workflow** that auto-generates new tasks and stores them in a database

When the user scans the QR code, the website retrieves a task from the task database and displays it instantly.  
The database is continuously updated through AI-generated tasks, ensuring there is always variety.

---

## 2. n8n Workflow: Automated Task Generation

The core logic lives in an n8n workflow.  
It runs automatically on a set interval — for example:

- every day  
- every morning at 09:00  
- every Saturday  
- or even every hour, depending on how many new tasks are needed

### 2.1 Scheduled Trigger

The workflow begins with a **Schedule Trigger**, which activates at the configured interval.  
This makes the system fully automated — no manual updates are needed.

### 2.2 Fetch Existing Tasks

After the trigger fires, the workflow checks the task database (currently **Google Sheets**, optionally **Supabase** later).  
It retrieves all tasks that already exist, including:

- previously generated tasks,  
- tasks manually added by the team,  
- disabled or archived tasks (optional).

This list provides the **context** needed for the AI Agent to avoid generating duplicates.

### 2.3 AI Agent: Generate New Tasks

Once the dataset is loaded, the workflow sends it to an **AI Agent node**.

The AI Agent is instructed to:

- produce **new social-interaction tasks**,  
- avoid duplicates,  
- keep them short and friendly,  
- follow the same style as existing tasks,  
- focus on low-pressure, accessible, positive prompts.

Because the full list of already existing tasks is provided, the AI can think:  
*“Create 5 new tasks that are not in this list.”*

This ensures each batch of tasks is unique.

### 2.4 Add New Tasks to the Database

After generating the new tasks, n8n writes them back into the database.  
Depending on backend setup, tasks are appended to:

- **Google Sheets**, used for prototyping,  
- or **Supabase**, used in production for faster syncing and API access.

Over time, the list grows into a large library of diverse prompts that the website can randomly select from.

---

## 3. Website & QR Code Flow

The QR code attached to Teddy directs people to a lightweight web page.

### When someone scans the code:

1. They open the website in their browser.  
2. The site requests a task from the database (e.g. via API or direct read).  
3. A random task is chosen from the list.  
4. The task is displayed as a friendly prompt.  

The user does the task, passes Teddy to someone else, and the cycle repeats.

This makes Teddy an interactive, social object that encourages positive micro-interactions throughout the community.

---

## 4. Benefits of This Approach

- **Unlimited tasks** thanks to AI generation  
- **Tasks stay unique** because duplicates are detected and avoided  
- **Easy to maintain** — n8n handles all automation  
- **Low-latency and lightweight** for the user (scan → task instantly)  
- **Scalable** — database and generation frequency can grow as needed  
- **Fun and human-centered** — small prompts that improve social connection  

---

## Conclusion

Teddy uses n8n, AI task generation and a simple QR-code interaction to create a playful experience that encourages meaningful social contact. The system keeps growing automatically as the AI adds new tasks, ensuring Teddy always brings a fresh and positive challenge wherever he goes.

---

## Images

<!-- <img src="/Images/Sprint1_Prototype/TeddyBear.png" width="300" style="border-radius: 12px;" /> -->

<div style="display: flex; gap: 50px;">
  <img src="Images/Sprint1_Prototype/TeddyBear.png" style="width: 33%;" />
  <img src="Images/Sprint1_Prototype/TeddyBear_QRCode.png" style="width: 60%;" />
</div>
