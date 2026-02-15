# Binding Syntax Reference

Quick reference for channel binding configuration during orchestration design.

---

## Binding Priority (Most-Specific Wins)

1. **Peer match** (exact DM/group id) — highest priority
2. **Guild/Team id** (Discord guild, Slack team)
3. **Account id** (specific channel account)
4. **Channel-level** (any account on this channel)
5. **Default agent** — lowest priority (fallback)

**Key Rules:**
- More specific bindings MUST come before less specific ones in the config
- Peer bindings always win over channel-wide rules
- Only one agent handles each binding (no fan-out)

---

## Binding Examples

```json5
// Peer-level binding (most specific)
{
  agentId: "{agent-id}",
  match: {
    channel: "{channel}",
    accountId: "{account-id}",
    peer: { kind: "{direct|group}", id: "{peer-id}" },
  },
}

// Account-level binding
{
  agentId: "{agent-id}",
  match: {
    channel: "{channel}",
    accountId: "{account-id}",
  },
}

// Channel-level binding (least specific)
{
  agentId: "{agent-id}",
  match: { channel: "{channel}" },
}
```

---

## DM Split Configuration

Route different DMs to different agents based on sender id:

```json5
// Per-sender binding
{
  agentId: "{agent-id}",
  match: {
    channel: "whatsapp",
    peer: { kind: "direct", id: "+15551234567" },
  },
}
```

---

## Group Chat Mention Gating

```json5
{
  agents: {
    list: [
      {
        id: "{agent-id}",
        groupChat: {
          mentionPatterns: ["@{pattern1}", "@{pattern2}"],
        },
      },
    ],
  },
}
```

---

## Channel Access Control

```json5
{
  channels: {
    whatsapp: {
      dmPolicy: "allowlist",
      allowFrom: ["+15551234567", "+15559876543"],
    },
  },
}
```

---

## Supported Channels

WhatsApp, Telegram, Discord, Signal, iMessage, Slack, Webchat
