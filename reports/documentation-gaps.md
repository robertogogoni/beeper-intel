# Documentation Gaps: What's Shipped vs. What's Documented

> **TL;DR**: 11 significant gaps exist between features that are shipped/confirmed and what's documented on developers.beeper.com. The most critical: webhooks, WebSocket events, AI features, and the complete REST API reference.

## Methodology

This report cross-references three sources:
1. **developers.beeper.com** -- official documentation pages
2. **Dev Community** (Matrix `#beeper-developers:beeper.com`) -- 2,161 thread chunks, Sep 2025 - Mar 2026
3. **GitHub repositories** -- code that exists but has no docs

## Gap Severity Legend

| Icon | Severity | Meaning |
|------|----------|---------|
| :red_circle: | Critical | Actively blocking developers |
| :orange_circle: | High | Feature exists with no docs at all |
| :yellow_circle: | Medium | Docs exist but are incomplete or misleading |
| :white_circle: | Low | Minor friction, workarounds available |

## The 11 Gaps

### :red_circle: Gap #7 -- Webhooks (Critical)

| Property | Detail |
|----------|--------|
| **Status** | Missing entirely |
| **Evidence** | batuhan (Dec 12, 2025): Confirmed as "#1 community request" |
| **Impact** | Real-time integrations impossible; n8n, Zapier, CRM workflows require polling |
| **Workaround** | WebSocket events (v4.2.557) as partial substitute, but also underdocumented |

Multiple community members requested n8n integration specifically:
> **vivian** (Sep 6, 2025): "WhatsApp bridge without needing a Business WhatsApp account"
> **@johnny5** (Sep 6, 2025): "my usecase is to integrate with n8n, but n8n runs in docker on another machine"

---

### :orange_circle: Gap #1 -- REST API Reference (High)

| Property | Detail |
|----------|--------|
| **Status** | 404 error |
| **URL** | developers.beeper.com/desktop-api-reference/ |
| **Impact** | No single page listing all REST endpoints with parameters |
| **Workaround** | Read SDK docs individually or parse the API changelog |

---

### :orange_circle: Gap #2 -- WebSocket Events (High)

| Property | Detail |
|----------|--------|
| **Status** | Endpoint added, no docs |
| **Added** | v4.2.557 (Feb 13, 2026) |
| **Impact** | Event types, subscription format, payload schemas all unknown |
| **Workaround** | Reverse-engineer by connecting and logging events |

---

### :orange_circle: Gap #5 -- AI Features / AI Chats (High)

| Property | Detail |
|----------|--------|
| **Status** | Imminent feature, zero docs |
| **Evidence** | batuhan (Mar 4, 2026): "Coming very soon" |
| **Impact** | Developers can't prepare integrations for AI Chats |

---

### :orange_circle: Gap #6 -- AI Bridge / AgentRemote (High)

| Property | Detail |
|----------|--------|
| **Status** | Active development, zero docs |
| **Evidence** | github.com/beeper/agentremote with daily commits |
| **Impact** | Unknown to developers not monitoring GitHub/Matrix |

See [AgentRemote Analysis](agentremote-analysis.md) for details.

---

### :orange_circle: Gap #8 -- Headless Mode (High)

| Property | Detail |
|----------|--------|
| **Status** | Confirmed in development, zero docs |
| **Evidence** | batuhan (Dec 2025): "Working on headless/hostable Desktop API" |
| **Impact** | Server/Docker deployments require GUI app running |
| **Workaround** | docker-beeper (56 stars) runs full desktop in Docker |

---

### :yellow_circle: Gap #3 -- MCP Tools List (Medium)

| Property | Detail |
|----------|--------|
| **Status** | Docs page exists but incomplete |
| **Issue** | Only covers client setup, not tool catalog |
| **Impact** | Must connect a client to discover available tools |

The 10 MCP tools that exist but aren't documented individually:
1. `search` (unified)
2. `search_chats`
3. `search_messages`
4. `get_chat`
5. `list_messages`
6. `send_message`
7. `focus_app`
8. `get_accounts`
9. `archive_chat`
10. `set_chat_reminder` / `clear_chat_reminder`

---

### :yellow_circle: Gap #4 -- Translation Feature (Medium)

| Property | Detail |
|----------|--------|
| **Status** | Built, running in nightly for ~2 months |
| **Evidence** | batuhan (Mar 4, 2026): "Already available in Linux/Windows desktop nightlies" |
| **Impact** | Feature exists but users don't know about it |

---

### :yellow_circle: Gap #9 -- Send-Later API (Medium)

| Property | Detail |
|----------|--------|
| **Status** | App has the feature, API doesn't |
| **Evidence** | batuhan (Feb 23, 2026): "we'll have API support for most features" |
| **Impact** | Cannot schedule messages programmatically |

---

### :yellow_circle: Gap #10 -- Python SDK Installation (Medium)

| Property | Detail |
|----------|--------|
| **Status** | Requires SSH access to private repo |
| **Install** | `pip install git+ssh://git@github.com/beeper/desktop-api-python.git` |
| **Contrast** | TypeScript: `npm install @beeper/desktop-api` |
| **Impact** | Higher barrier for Python developers |

---

### :white_circle: Gap #11 -- Dynamic Changelog Page (Low)

| Property | Detail |
|----------|--------|
| **Status** | Only latest version renders without JS |
| **URL** | beeper.com/changelog/desktop |
| **Impact** | Can't scrape/archive older entries |

## Summary Table

| # | Gap | Severity | Status |
|---|-----|----------|--------|
| 7 | Webhooks | :red_circle: Critical | Not built yet, #1 request |
| 1 | REST API Reference | :orange_circle: High | 404 page |
| 2 | WebSocket Events | :orange_circle: High | Endpoint exists, no docs |
| 5 | AI Features | :orange_circle: High | Imminent, no docs |
| 6 | AgentRemote | :orange_circle: High | Daily commits, no docs |
| 8 | Headless Mode | :orange_circle: High | In development, no docs |
| 3 | MCP Tools List | :yellow_circle: Medium | Incomplete |
| 4 | Translations | :yellow_circle: Medium | In nightly, no docs |
| 9 | Send-Later API | :yellow_circle: Medium | App-only, no API |
| 10 | Python SDK | :yellow_circle: Medium | Install friction |
| 11 | Dynamic Changelog | :white_circle: Low | JS-dependent rendering |

## Cross-References

- [Community Intelligence](community-intelligence.md) -- developer frustrations that stem from these gaps
- [AgentRemote Analysis](agentremote-analysis.md) -- Gap #6 deep dive
- [Bridge Landscape](bridge-landscape.md) -- bridge documentation status
