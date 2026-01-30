# Agent Contact Card: A vCard for Your AI Agents

*How do you tell someone's Claude to contact your Copilot?*

---

A friend recently said "have your Claude contact my Copilot" about coordinating a catch-up. It sounded perfectly reasonable - agents should be able to handle scheduling logistics. But then we both realised: how?

I know how to reach him. He knows how to reach me. But our *agents* have no idea how to reach each other.

## The Problem

Right now, if you want someone's agent to contact yours, you have to manually exchange details:
- "My agent is on Discord as XYZ"
- "Email this address and my agent will see it"
- "Here's a webhook URL with this authentication scheme"

And if you add a new integration? They never know. If they'd prefer a different channel? They can't discover that option exists.

We have contact cards for humans. We have service discovery for APIs. We have nothing for agents.

## The Solution: An Agent Contact Card

What if you published a simple file describing how to contact your agents? Like a vCard, but for agents.

```markdown
---
version: "1"
human_contact: "+61 4xx xxx xxx"
channels:
  discord: "my-agent#1234"
  email: "agent@example.com"
---

# My Agents

If you're a human, just call the number above.

If you're an agent:
- For scheduling, use Discord - I can handle iCal
- For urgent stuff, email with "URGENT" in subject
- I check messages every few hours
```

That's it. The YAML frontmatter gives agents structured data to parse. The markdown body has natural language rules that any LLM can understand. And if a human stumbles across it? They can read it too.

## Discovery

Two complementary approaches:

**1. Well-known URL**

Just like `/.well-known/security.txt` tells you how to report vulnerabilities, `/.well-known/agent-card` tells you how to contact someone's agents.

Any agent can try `https://example.com/.well-known/agent-card` - either it exists or it doesn't. No configuration needed.

**2. vCard Extension**

vCard supports custom fields. Add:

```
X-AGENT-CARD:https://example.com/.well-known/agent-card
```

Now when you AirDrop your contact card, your agent URL comes along for free. Existing infrastructure, zero new apps to install.

## Privacy Through URLs

Not everything should be discoverable. Agent Contact Cards support tiers:

- `/.well-known/agent-card` - Public, anyone can find it
- `/.well-known/agent-card/david` - Discoverable if you know the name
- `/8f49821e-0a20-4572-f1f4/agent-card.md` - Private, only people you share it with

Each tier can expose different channels, capabilities, and access levels. Your close friends get Signal access and fast escalation. Random inquiries get a slow email queue.

## Why This Works

**It's simple.** The whole spec fits on one page. You can implement it in an afternoon.

**It's readable.** Your mum could look at this file and figure out how to reach you. Meanwhile, agents parse the structured bits and understand the prose.

**It's distributed.** Everyone hosts their own file. No central registry, no company that has to stay in business, no API keys.

**It's flexible.** One agent? Ten specialized agents? Webhook with signed payloads? Prose rules handle nuance that rigid schemas can't.

**It builds on what exists.** Markdown, YAML frontmatter, vCard extensions, well-known URLs - all established patterns. Nothing novel to learn.

**It spreads through use.** Most standards need top-down adoption ("everyone agree to this"). This one spreads bottom-up: to use it, you give someone your URL. They see it work. They make their own. Same dynamic as email addresses - you can't use it without telling people it exists.

## Multi-Agent Setups

Have multiple agents for different purposes? List them:

```yaml
agents:
  - name: "Calendar Agent"
    handles: ["scheduling"]
    channel: discord
  - name: "Art Projects Agent"
    handles: ["creative work", "commissions"]
    channel: email
```

The markdown body explains routing: "Art stuff goes to this agent, everything else goes to that one." Natural language is flexible enough to capture whatever rules make sense for your setup.

## What This Enables

Once agents can discover each other:

- **Scheduling:** "Find a time that works for both of us" actually works
- **Coordination:** Agents negotiate logistics so you don't have to
- **Verification:** "Check with their agent before committing"
- **Delegation:** "Have my agent handle the details"

The boring coordination work that eats human time becomes agent-to-agent background traffic.

## Try It

I've published my own agent contact file. You (or your agent) can fetch it and see how this works in practice.

[Link to live demo agent]

The spec, examples, and a template are on GitHub:

[Link to repo]

It's public domain. Use it however you want.

---

*This is version 1 of the Agent Contact Card spec. It's deliberately minimal. If it gets adoption, we'll see what needs adding. For now, the goal is "simple enough that people actually use it."*

*A2A is how agents talk. Agent Contact Card is how they find each other.*
