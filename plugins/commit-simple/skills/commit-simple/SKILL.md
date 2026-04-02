---
name: commit-simple
description: Quick commit workflow that stages and commits changes with a clean, short commit message. Use this skill whenever the user asks to commit, make a commit, save changes, or says /commit. Also use when the user says "commit this", "committni to", "commitni", or any variation of requesting a git commit.
---

# Commit Simple

A fast commit workflow: analyze changes, compose a short message, stage relevant files, and commit.

## Rules

1. **Never mention Claude, AI, LLM, or Anthropic** in the commit message. No Co-Authored-By lines. The commit must read as human-written.
2. **Never commit files in `docs/` folder** (plans, analysis documents, etc.). Silently skip them.
3. **Keep the message short.** One summary line, optionally followed by a blank line and 1-3 short bullet points if the change is non-trivial.

## Commit message format

Follow the conventional commits style used in this repo:

```
type(scope): short summary

- optional detail line
- optional detail line
```

**Types:** `feat`, `fix`, `refactor`, `chore`, `config`, `test`, `docs`
**Scope:** service or component name (e.g., `kbs`, `worker`, `eval`, `chatbot`)

The summary line should be under 72 characters and describe the "what" concisely. Use lowercase. No trailing period.

**Examples:**

```
feat(kbs): add context vector search and parallelise retrieval pipeline
```

```
fix(worker): handle missing embeddings gracefully

- skip chunks with empty content
- log warning instead of failing the batch
```

## Workflow

1. Run `git status` (never use `-uall`) and `git diff` (staged + unstaged) in parallel to understand all changes.
2. Also run `git log --oneline -5` to match the repo's recent commit style.
3. Identify which files to stage. **Exclude:**
   - Everything under `docs/` (plans, analysis)
   - Files that look like they contain secrets (`.env`, credentials)
4. Compose the commit message based on the actual changes. Pick the right type and scope.
5. Present the proposed commit message and list of files to be staged to the user. Wait for confirmation.
6. After user confirms: stage the files, create the commit using a HEREDOC for the message, then run `git status` to verify.

If there are no meaningful changes to commit, say so and stop.
