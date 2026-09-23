---
name: x-handoff
description: Hand a Codex discovery, build experience, or release from the current task to a dedicated X Content Desk. Use when the user asks to share, draft, or publish it on X without restating its context.
---

# Hand off work from the source task

The source task has the project context. Do not ask the user to rewrite it or switch tasks.

1. Identify the shareable story: a discovery, a build experience, or a release. Capture what prompted it, what the user tried or learned, and the outcome. Distinguish facts evidenced by the conversation, files, tests, or links from interpretation and open questions. A personal observation need not have a public repository, but must be grounded in what the user actually said or did. Preserve the user's exact wording about drafting versus publishing.
2. Spawn one subagent to prepare the X handoff from this task's context. Choose an available model suited to routine research and writing; give the subagent the relevant conversation context and source paths or links. The subagent must exclude secrets, private user data, and unverified claims.
3. The subagent uses `mcp__codex_app__list_threads` to find exactly one pinned task named `X 内容编辑台` or `X Content Desk` (or the desk title the user named). Use its returned `threadId` and `hostId` with `mcp__codex_app__send_message_to_thread`. Do not guess a task ID. If the desk is missing or ambiguous, report that in the source task and keep the prepared handoff there.
4. Send a concise, self-contained message: source task title/ID if known; user's exact request; story type and angle; target audience and suggested language; grounded facts with relevant links or paths; uncertainties and sharing limits; and one draft post. State `publish` when the user explicitly says to post this item to X, including “把这个发到 X”; otherwise state `draft`. The desk verifies its configured account before publishing.
5. Confirm that the destination accepted the message, then tell the user in the source task that the handoff reached the desk. The subagent does not publish to X itself.

The X Content Desk owns final copy, duplicate checks, posting, and its ledger. A handoff is not proof that a post was published.
