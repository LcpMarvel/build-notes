# Build Notes

[简体中文](README.zh-CN.md)

This Codex plugin shares discoveries, build experiences, and releases from your Codex tasks. In the task with the relevant context, say **“Post this to X.”** A subagent prepares a grounded handoff from that task. A dedicated X Content Desk checks the copy and signed-in account, publishes the post, and records its URL.

## How it works

1. [`x-handoff`](skills/x-handoff/SKILL.md) extracts the story, audience, grounded facts, sources, uncertainties, and a draft from the source task. It sends them to one pinned task named `X Content Desk` or `X 内容编辑台` using Codex task tools.
2. [`x-editor`](skills/x-editor/SKILL.md) checks the sources and prior posts. It drafts only unless the user's instruction explicitly requested publication of this result.
3. When publishing is authorized, the desk verifies the signed-in X account, posts through an available browser tool, confirms the result on the profile, and reports the post URL.

The plugin does not copy entire conversations between tasks. The source subagent prepares the relevant context, so the user does not have to restate the project.

## Install

This repository includes a portable `plugin.json`, a Codex compatibility manifest, two skills, and `.agents/plugins/marketplace.json`. Install from [LcpMarvel/build-notes](https://github.com/LcpMarvel/build-notes):

```bash
codex plugin marketplace add LcpMarvel/build-notes
codex plugin add build-notes@build-notes
```

To test a local checkout instead, run these from its root:

```bash
codex plugin marketplace add .
codex plugin add build-notes@build-notes
```

See the [OpenAI plugin packaging guide](https://developers.openai.com/plugins/build/plugins) for installation details.

## One-time setup

1. Create and pin a long-lived Codex task named `X Content Desk` or `X 内容编辑台`.
2. Tell that task which X account it manages, the preferred languages, and where to keep its post ledger.
3. Sign in to that X account in a browser that Codex can use. The plugin stores no credentials.

The host needs subagents and Codex task tools for handoff, plus browser control for publishing. If one is unavailable, the workflow keeps a draft and reports the missing capability.

## Use from any Codex task

- **Publish:** “Post this to X.” This is an instruction to publish the specific discovery or experience in the source task.
- **Draft only:** “Send this to X Content Desk as a candidate post.”

The desk verifies sources, account, and duplicates before publishing. It follows browser and action-time approval requirements and never treats a click attempt as proof of publication. Build Notes runs only when you trigger it in a task; it does not monitor tasks or schedule posts in the background. It does not bundle X API access, passwords, cookies, or keys.

Version `0.1.0` has passed local manifest and skill-structure checks. The full cross-task publishing flow still needs a live test after installation. No license has been selected yet. The current owner's post ledger is kept in Git-ignored `CONTENT.md` and is not part of the distributed plugin.
