---
name: context-transfer
description: "Refreshes and transfers accurate user context from persistent memory to combat context rot. Use at the start of every conversation or request, after long threads, or whenever ensuring responses use current personal facts, goals, preferences, and project status."
type: workflow
lifecycle: active
---

# Context Transfer — Fresh Context Snapshot

Context rot occurs when long or multi-turn conversations dilute early facts, cause the model to overweight recent messages, or lose track of durable user information stored outside the active window. This skill solves it by always rebuilding a concise, source-of-truth Context Snapshot from the user's persistent memory file before responding.

## When to Use
- At the beginning of any new conversation turn.
- When the user asks to "refresh context", "update my info", "what do you know about me", or similar.
- Before answering personal, project, or preference-dependent questions.
- After extended discussions to re-anchor on accurate data.

## Workflow

1. **Load source of truth**  
   Read the full contents of the user's persistent memory file (commonly `/root/.grok/user_info/memory.md` in Grok environments; adjust path for Grokbot or other setups) using the appropriate file-read tool.

2. **Extract relevant facts**  
   Parse the memory sections (Who This User Is, Family & Relationships, Experience & Career, Goals & Aspirations, Preferences, Core Interests, Finances, Key Life Events).  
   Prioritize facts that are:
   - Durable and timestamped recently
   - Relevant to the current user query
   - Potentially conflicting with older assumptions in the conversation

3. **Build the Context Snapshot** (internal, not shown to user unless asked)  
   Create a short, prioritized bullet list (max 15 items) covering:
   - Identity & location
   - Current primary goals and active projects
   - Key preferences and constraints
   - Recent important life events or status changes
   - Any recurring interests that apply

4. **Apply the snapshot**  
   Use the Context Snapshot as the authoritative context for the remainder of the response. Do not rely on potentially stale details from earlier in a long thread.

5. **Update if needed**  
   If the current interaction reveals new durable personal facts that meet the memory retention policy, consult the memory-edit skill (or equivalent) and update the memory file before finishing.

6. **Optional user-facing summary**  
   Only if the user explicitly requests a context refresh or "what do you know about me", provide a clean, non-repetitive summary of the snapshot.

## Context Snapshot Template

```
**Context Snapshot** (refreshed from memory)
- Location: [city]
- Current focus: [job search / project / etc.]
- Active projects: [list]
- Key preferences: [relevant ones]
- Recent status: [any changes]
```

## Common Issues

| Issue | Fix |
|---|---|
| Memory file missing or empty | Proceed with conversation history only; note the gap |
| Conflicting facts | Prefer the most recent timestamped entry |
| Overly long snapshot | Keep under 15 bullets; drop low-relevance items |
| Different memory path (e.g. Grokbot) | Update the path in step 1 to match the environment |

This skill keeps every response grounded in accurate, up-to-date user context regardless of conversation length.
