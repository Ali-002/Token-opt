# Code Token Management Hacks

From what I have learned so far:

## Tier 1: Easy Techniques

### 1. Start Fresh Conversations (`/clear`)

- Use `/clear` when switching to a different task.
- This prevents GitHub Copilot from reloading irrelevant chat history.

### 2. Disconnect Unused MCP Servers

- Every connected MCP server loads its tool definitions into context on each message.
- Unused MCP servers create invisible token overhead.
- Prefer CLI tools where possible.

### 3. Batch Instructions into a Single Prompt

**Quality is more important than cost.**

- Combine related requests into one message.
- Bad: “Summarize” → “Find issues” → “Suggest fixes”.
- Good: “Summarize, find issues, and suggest fixes.”
- This reduces repeated context processing.
- Adding the right context can increase the cost of one request while reducing the total number of interactions.

### 4. Use Plan Mode First

- Have GitHub Copilot create a plan before making changes.
- Planning encourages clarification and reduces costly mistakes.
- This prevents tokens from being wasted on incorrect implementations.

### 5. Check `/context` and `/cost`

- `/context` shows what is consuming tokens.
- `/cost` shows current token usage and spending estimates where supported, such as Claude.
- These commands make hidden token consumption visible.

### 6. Configure a Status Line

For tools that support it, display:

- The current model.
- Token count.
- Context usage percentage.

This provides real-time visibility into session growth.

### 7. Keep Your Usage Dashboard Open

- Monitor remaining allocation and reset times.
- This helps pace usage and avoid unexpected limits.

### 8. Be Selective When Pasting Content

- Provide only the relevant code, text, or document sections.
- Do not paste an entire file when one function is enough.
- Less input generally means fewer tokens.

### 9. Watch GitHub Copilot While It Runs

- Monitor long-running tasks.
- Stop execution if it starts looping or exploring the wrong path.
- This can save substantial token usage.

## Tier 2: Intermediate Techniques

### 10. Keep `.github/copilot-instructions.md` Lean

- Keep it under approximately 200 lines.
- Include only the technology stack, coding standards, build commands, and critical project rules.
- Treat it as an index, not a knowledge base.

### 11. Use Precise File References

- Point the agent directly to relevant files and functions.
- Example: “Check `verifyUser()` in `auth.js`.”
- Avoid vague requests such as “Search the entire repository.”
- Relevant context is better than more context; quality correlates with relevance, not volume.

### 12. Compact Early

- Do not wait for automatic compaction at approximately 95% context usage.
- Run `/compact` while the context is still healthy.
- This helps maintain output quality and reduce context bloat.

### 13. Avoid Long Idle Periods

- Context caching can expire after several minutes.
- Returning later may require large amounts of context to be reprocessed.
- Consider compacting or clearing the conversation before stepping away.

### 14. Control Command Output Bloat

- Shell command output becomes part of the conversation context.
- Large logs and verbose results consume many tokens.
- Restrict commands and output to what is necessary.

## Tier 3: Advanced Optimization

### 15. Choose the Right Model

- Use a smaller model for simple tasks such as formatting and summarization.
- Use a general-purpose coding model for routine development work.
- Use a stronger reasoning model for architecture and deep analysis.
- Use the smallest model capable of completing the task well.
- Reasoning models can damage good plans by reconsidering decisions that were already correct during implementation.
- Cheaper models often execute better when the specification is complete and precise.
- The most expensive model is not automatically the best model.

### 16. Keep Instructions Non-Negotiable

Instructions should contain only rules that are genuinely non-negotiable. Every instruction is paid for repeatedly, so optional preferences and background information should be kept elsewhere.

### 17. Treat Instructions as a High-Leverage Location

Instructions appear near the beginning of the context, where model attention is strongest. Put the most important constraints there.

### 18. Prevent Known Failures

Use instructions primarily to prevent recurring mistakes. A short rule that addresses a known failure is more valuable than broad, generic advice.

### 19. Avoid AI-Generated Instruction Bloat

AI-generated instructions tend to become bloated. Human-written instructions are usually more precise, so review generated rules critically before adding them.

### 20. Refine Instructions Continuously

Treat instructions like production code: review, test, and improve them as the project changes.

### 21. Delete Instructions Aggressively

Remove outdated or redundant rules. Old instructions become noise and can lower response quality.

### 22. Rebuild Instructions Periodically

The Copilot CLI team reportedly rebuilds its instructions periodically. Refreshing the file from current needs can be more effective than endlessly accumulating rules.

## Optional Optimization

Pre-filter data before giving it to agents. Clean data beats raw data, and high signal density improves agent performance.

## Chronicle Note

I saw advice recommending [Chronicle](https://github.com/theagentplane/chronicle), but I have not tried it yet. Let me know if anyone is interested in testing it.

## General Tips

- Avoid running at 80–100% context capacity; the model may start drifting from the system instructions and original objectives.
- Prefer relevant, high-signal context over more context.
- Keep prompts focused and remove unnecessary history when starting a new task.

> **Key takeaway:** Token management is largely a context-hygiene problem, not a plan-limit problem.

