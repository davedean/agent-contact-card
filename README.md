# Agent Contact Card

A simple, open format for discovering how to contact someone's AI agents. Like a vCard, but for agents.

## The Problem

Your friend says "have your Claude contact my Copilot" - but how? There's no way to discover how to reach someone's agents. You have to manually exchange Discord IDs, email addresses, webhook URLs... and if they add a new integration, you never know.

## The Solution

An Agent Contact Card - a markdown file at a known URL that describes how to contact someone's agents.

```markdown
---
version: "1"
human_contact: "+61 4xx xxx xxx"
channels:
  discord: "myagent#1234"
  email: "agent@example.com"
---

# My Agents

If you're a human, just call the number above.

If you're an agent:
- For scheduling, use Discord - I can handle iCal
- For urgent stuff, use email with "URGENT" in subject
- I check messages every few hours
```

That's it. Humans can read it. Agents can parse the frontmatter and understand the prose rules.

## Discovery

**Option 1: Well-known URL**

Check `https://example.com/.well-known/agent-card` for any domain.

**Option 2: vCard extension**

Add an `X-AGENT-CARD` field to your contact card:
```
X-AGENT-CARD:https://example.com/.well-known/agent-card
```

Now when you share your contact info, your agent URL comes along for free.

## Quick Start

1. Copy an [example](examples/) file
2. Edit it with your agent's contact info
3. Host it at `/.well-known/agent-card` on your domain (or any URL)
4. Add `X-AGENT-CARD:your-url` to your vCard

## Spec

See [spec.md](spec.md) for the full specification.

## Examples

- [Personal agent](personal.md) - Individual with a few contact channels
- [Organization](organization.md) - Company with multiple specialized agents
- [Minimal](minimal.md) - Simplest possible valid file

## Why Markdown?

- Humans can read it (your mum could figure it out)
- Agents can parse the YAML frontmatter for structured data
- Agents can understand the prose rules (any decent LLM can)
- Easy to author (no special tools needed)
- Established format (same as Jekyll/Hugo/Obsidian frontmatter)

## License

Public domain. Use it however you want.
