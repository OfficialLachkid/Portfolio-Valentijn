# AI Context Workflow at Domits

<div style="text-align: center; margin: 0.2rem 0 1rem;">
  <img
    src="Images/Domits_Internship/Domits_Logo.png"
    alt="Domits logo"
    style="display: inline-block; width: 120px; max-width: 100%; height: auto;"
  />
</div>

<div style="text-align: center; margin: 0.25rem 0 1.75rem;">
  <img
    src="Images/Domits_Internship/Images/Direct_Booking_Website/Obsidian_Brain_Graph.png"
    alt="Obsidian brain graph view"
    style="display: inline-block; width: 820px; max-width: 100%; height: auto; border-radius: 18px;"
  />
</div>

## Overview
During my internship at [Domits](https://www.domits.com/), part of my contribution was not only building product features, but also improving how AI was used in day-to-day engineering work. This was not a task that was handed to me as a separate assignment. I set this up myself because I wanted working with AI to become more practical, easier to start correctly, and easier to keep aligned with ongoing implementation work.

The Obsidian-based vault became a durable context layer so that important knowledge did not stay trapped in scattered chats, temporary memory, or one-off debugging sessions. It also gave me a clearer way to keep my own work, discoveries, and active task context updated while moving across multiple features and branches.

This workflow mattered because the product surface at Domits was broad. Work moved across host tooling, guest flows, bookings, direct booking websites, integrations, and release work. In that kind of environment, a large part of engineering cost is not typing code. A large part of engineering cost is recovering context: understanding how the system works, what decisions already exist, which trade-offs were chosen, and where the real risks are.

## Why I Started This Myself
I noticed that AI became far more useful when the starting context was shaped on purpose instead of rebuilt from scratch in every session. Without that, too much time was lost repeating background, re-explaining decisions, or re-finding the same implementation details.

I wanted to improve three things in practice:

- make it easier for someone to start a useful AI session without first rebuilding the whole product context manually
- make AI support more practical for real engineering work instead of generic prompt experimentation
- make it easier to keep my own work, decisions, and active implementation state updated in a reusable way

That made the workflow useful both as a team aid and as a way to reduce context loss in my own ongoing work.

In other words, I was not only trying to make AI "available." I was trying to make it usable. The difference matters. A tool can exist in a team without being practical to start with, practical to trust, or practical to maintain over time. This workflow was meant to lower that friction.

## Why The Obsidian Vault Existed
The vault existed as a shared starting point for both developers and AI-assisted work. The goal was not to let AI guess the codebase from scratch in every new chat. The goal was to provide enough stable context that AI could reason faster, stay aligned with product reality, and avoid repeating mistakes the team had already learned from.

The vault was useful because it kept durable knowledge close to the repository without mixing it into production code. It served as a reusable context layer for:

- product understanding
- engineering rules and conventions
- active feature context
- known risks and recurring bug patterns
- handoff continuity between people, branches, and sessions

## How The Workflow Worked In Practice
The normal flow was to start narrow instead of blind. A new AI session did not begin only from a prompt. It began from a small set of stable sources first, and then moved into the repository files.

The startup path was intentionally simple:

1. `README.md`
2. core context notes such as `Domits_Context.md`
3. the relevant working or feature note
4. repository code and implementation files

This gave AI a grounded orientation before it started making code-level decisions.

The workflow also followed a clear rule: the vault helps with orientation, but the repository is still the final source of truth. If a vault note and the implementation ever disagreed, the code won and the vault needed to be updated.

## Why This Approach Was Better
This workflow improved the quality of AI-assisted engineering in several ways.

### Faster Onboarding
New developers and new AI chats did not need to rediscover the same background repeatedly. Product context, workflow rules, and feature history were easier to recover.

### Better Continuity
AI chats are temporary, but project knowledge should not be temporary. The vault reduced the chance that useful engineering understanding disappeared after a single session ended.

### Less Repetition
The team did not need to keep re-explaining the same feature history, deployment constraints, or architectural rules every time a new task started.

### Better Output Quality
AI performs better when it understands the project's naming, structure, domain language, and active scope. That reduced wrong assumptions and wasted implementation loops.

### Stronger Handoffs
This was especially useful in an internship setting, where continuity matters. Important knowledge became easier to hand off instead of depending on one person still being around to explain it.

### Easier Starts For Other Users
It also made it easier for other developers or AI users to begin work from a clearer starting point. Instead of beginning from a blank chat and manually reconstructing context, they could begin from a smaller, more reliable set of notes and move into the codebase with less friction.

## Trade-Offs We Accepted Deliberately
This workflow was useful, but it also came with responsibilities.

- Context maintenance costs time, but repeated rediscovery costs more.
- Not every note belongs in the vault, because uncurated information reduces retrieval quality.
- Stale notes are dangerous, so durable notes need correction when repo reality changes.
- AI still needs human judgment; it can accelerate work, but it should not replace accountability.

## Why I Included This In My Portfolio
I included this workflow because it shows another side of my internship contribution. My work at Domits was not only about features and interfaces. It also included proactively improving how engineering knowledge could be stored, reused, and handed over in a team that was moving across many active workstreams.

For me, this was valuable because it combined:

- technical implementation work
- product and architecture context management
- AI-assisted engineering practices
- easier onboarding for AI-assisted work
- better handoffs and lower context loss

That makes it a strong example of contributing not only to the product itself, but also to the way the engineering team worked around that product.
