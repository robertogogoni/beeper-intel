# Bridge Landscape: Official + Community

> The complete catalog of Beeper bridges: 13 official networks, 5+ community bridges, registration providers, and the self-hosting ecosystem.

## Official Bridges (via mautrix)

All official bridges are maintained under the [mautrix](https://github.com/mautrix) organization, created by **tulir** (Beeper core developer). They use the Matrix bridgev2 interface.

| Network | Repository | In-App | Self-Host | Status |
|---------|-----------|--------|-----------|--------|
| WhatsApp | mautrix/whatsapp | Yes | Yes | Active |
| Telegram | mautrix/telegram | Yes | Yes | Active |
| Signal | mautrix/signal | Yes | Yes | Active |
| Facebook | mautrix/meta | Yes | Yes | Active |
| Instagram | mautrix/meta | Yes | Yes | Active |
| Discord | mautrix/discord | Yes | Yes | Active |
| Slack | mautrix/slack | Yes | Yes | Active |
| LinkedIn | mautrix/linkedin | Yes | Yes | Active |
| Google Messages | mautrix/gmessages | Yes | Yes | Active |
| Google Chat | mautrix/googlechat | Yes | Yes | Active |
| X / Twitter | mautrix/twitter | Yes | Yes | Active |
| iMessage | beeper/platform-imessage | Yes | Limited | Active (Swift, daily commits) |
| Google Voice | mautrix/gvoice | No | Yes | Not in app |
| Bluesky | mautrix/bluesky | No | Yes | Not in app |
| Android SMS | gitlab.com/beeper/android-sms | No | Limited | Not in app |

## iMessage: A Special Case

iMessage bridging is uniquely complex due to Apple's restrictions:

| Component | Stars | Language | Purpose |
|-----------|-------|----------|---------|
| [platform-imessage](https://github.com/beeper/platform-imessage) | 1 | Swift | On-device iMessage for Desktop (daily commits) |
| [barcelona](https://github.com/beeper/barcelona) | 70 | Swift | Swift iMessage framework |
| [imessage](https://github.com/beeper/imessage) | 1032 | Go | Original bridge (ARCHIVED) |
| [mac-registration-provider](https://github.com/beeper/mac-registration-provider) | 150 | Go | Registration data from Mac |
| [phone-registration-provider](https://github.com/beeper/phone-registration-provider) | 119 | Logos | Registration on jailbroken iPhone |
| [registration-relay](https://github.com/beeper/registration-relay) | 35 | Go | Registration data relay |

### Community iMessage

| Component | Stars | Language | Purpose |
|-----------|-------|----------|---------|
| [lrhodin/imessage](https://github.com/lrhodin/imessage) | 23 | Rust | v2 rewrite using rustpush/bridgev2 (very active) |

**Notable**: lrhodin submitted bridge-manager PR #73 to add `imessage-v2` bridge type (closed, not merged).

## Community Bridges

| Bridge | Author | Stars | Network | Status |
|--------|--------|-------|---------|--------|
| [Heisenbridge](https://github.com/hifi/heisenbridge) | hifi (Beeper) | - | IRC | Active, v1.14.2 with websocket |
| [matrix-line-messenger](https://github.com/highesttt/matrix-line-messenger) | highesttt | 14 | LINE | Active |
| [snapchat-bridge](https://github.com/lalomorales22/snapchat-bridge) | lalomorales22 | 1 | Snapchat | Early stage |
| [zalo-beeper-bridge](https://github.com/lequocbinh04/zalo-beeper-bridge) | lequocbinh04 | 0 | Zalo | Early stage |
| [groupme](https://github.com/beeper/groupme) | beeper | 18 | GroupMe | Active |

## Bridge Bounty Targets

Beeper offers up to **$50,000** for new bridges. The following networks are eligible:

| Network | Estimated Demand | Bounty Potential |
|---------|-----------------|-----------------|
| WeChat | Very High | Up to $50K |
| Microsoft Teams | Very High | Up to $50K |
| Snapchat | High | Up to $50K |
| Viber | Medium | Up to $50K |
| LINE | Medium | Up to $50K |
| Bumble | Medium | Up to $50K |
| Tinder | Medium | Up to $50K |
| Hinge | Medium | Up to $50K |

**Requirements**: Matrix bridgev2 interface in Golang. Contact: kishan@beeper.com

> **Community voice** -- vinc (Sep 6, 2025): "I'd sacrifice a goat and give half my salary for a good Teams integration"

## Self-Hosting Ecosystem

### bridge-manager (bbctl)

| Property | Value |
|----------|-------|
| **Stars** | 1290 (most starred Beeper repo) |
| **Version** | v0.14.0 |
| **Platforms** | Linux, macOS (amd64/arm64), Windows via WSL |
| **Requirements** | Python 3 with venv, ffmpeg, Active Beeper account |
| **Data dir** | `~/.local/share/bbctl` |

### Community Self-Hosting Tools

| Tool | Stars | Description |
|------|-------|-------------|
| [beeper-bridges](https://github.com/rhinot/beeper-bridges) | 16 | Docker Compose for self-hosted bridges |
| [bridge-manager-multiarch](https://github.com/holysoles/beeper-bridge-manager-multiarch) | 0 | Multi-arch bridge-manager images |
| [docker-beeper](https://github.com/zachatrocity/docker-beeper) | 56 | Full Beeper Desktop in Docker |

### Open Bridge-Manager PRs

| PR | Author | Title | Status |
|----|--------|-------|--------|
| #72 | batuhan | Add AI bridge | OPEN |
| #68 | elsiehupp | Packaging | OPEN |
| #73 | lrhodin | Add imessage-v2 bridge type | CLOSED (not merged) |

## AI Bridges (AgentRemote)

A new category of bridges connects AI agents to Beeper. See [AgentRemote Analysis](agentremote-analysis.md).

| Bridge | Agent | Status |
|--------|-------|--------|
| `bridges/ai` | Generic AI | Near ready |
| `bridges/codex` | OpenAI Codex | Near ready |
| `bridges/openclaw` | OpenClaw | Near ready |
| `bridges/opencode` | OpenCode | In development |

## Self-Hosted Bridges Community Insights

From the Self-hosted bridges Matrix room (10,911 thread chunks, Feb 2023 - Mar 2026):

Key themes from 3 years of community discussion:
- **Bridge naming conflicts**: Running self-hosted alongside official requires careful naming
- **Resource usage**: Bridges can be memory-intensive, especially WhatsApp and Telegram
- **Registration complexity**: iMessage registration remains the most complex setup
- **Docker preference**: Community overwhelmingly prefers Docker Compose deployments
- **bridge-manager adoption**: bbctl simplified setup dramatically when released

## Cross-References

- [AgentRemote Analysis](agentremote-analysis.md) -- AI bridge deep dive
- [Ecosystem Map](ecosystem-map.md) -- visual bridge architecture diagram
- [Community Intelligence](community-intelligence.md) -- bridge-related discussions
