# API Evolution Timeline

> Tracking the Desktop API from its gRPC origins to the modern REST/v1 architecture with 21 endpoints.

## Version History

### v4.1.294 -- Oct 16, 2025

**The Great Migration: gRPC to REST**

This release marked the fundamental architecture shift from gRPC (`/v0`) to RESTful (`/v1`) endpoints.

| Before | After |
|--------|-------|
| gRPC protocol | REST/JSON |
| `/v0/*` routes | `/v1/*` routes |
| Protobuf schemas | OpenAPI spec |
| Single SDK approach | 6 auto-generated SDKs |

**Impact**: Opened the API to any HTTP client. Enabled Stainless auto-generation of SDKs.

---

### v4.2.499 -- Jan 23, 2026

**Message Editing & File Uploads**

New endpoints:

| Method | Endpoint | Description |
|--------|----------|-------------|
| `PUT` | `/v1/chats/{chatID}/messages/{messageID}` | Edit messages |
| `POST` | `/v1/assets/upload` | Upload file (multipart) |
| `POST` | `/v1/assets/upload/base64` | Upload file (base64) |

Schema changes:
- Message schema adds `type` and `linkedMessageID` fields
- Message attachment support via `uploadID`

---

### v4.2.509 -- Jan 27, 2026

**Media Serving**

New endpoint:

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/v1/assets/serve` | Stream assets with range requests |

Supports `mxc://`, `localmxc://`, and `file://` URI schemes.

---

### v4.2.557 -- Feb 13, 2026

**The Big Feature Drop: WebSockets, Reactions, Discovery**

This was the largest single API update, adding 6 new endpoints:

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/v1/info` | Server discovery with metadata |
| `GET` | `/v1/ws` | WebSocket events with per-chat subscriptions |
| `POST` | `/v1/chats/{chatID}/messages/{messageID}/reactions` | Add reaction |
| `DELETE` | `/v1/chats/{chatID}/messages/{messageID}/reactions` | Delete reaction |
| `POST` | `/oauth/introspect` | Token introspection |
| `GET` | `/v1/accounts/{accountID}/contacts/list` | List contacts |

Schema changes:
- Chat creation supports `mode=start` for DMs
- Account schema no longer returns `network` field

---

## Current Endpoint Catalog (v4.2.557+)

### Discovery (2)

| Method | Endpoint | Added |
|--------|----------|-------|
| `GET` | `/v1/info` | v4.2.557 |
| `POST` | `/oauth/introspect` | v4.2.557 |

### Accounts (2)

| Method | Endpoint | Added |
|--------|----------|-------|
| `GET` | `/v1/accounts` | v4.1.294 |
| `GET` | `/v1/accounts/{accountID}/contacts/list` | v4.2.557 |

### Chats (5)

| Method | Endpoint | Added |
|--------|----------|-------|
| `GET` | `/v1/chats` | v4.1.294 |
| `POST` | `/v1/chats` | v4.1.294 |
| `GET` | `/v1/chats/{chatID}` | v4.1.294 |
| `PUT` | `/v1/chats/{chatID}/archive` | v4.1.294 |
| `PUT/DELETE` | `/v1/chats/{chatID}/reminder` | v4.1.294 |

### Messages (4)

| Method | Endpoint | Added |
|--------|----------|-------|
| `GET` | `/v1/chats/{chatID}/messages` | v4.1.294 |
| `POST` | `/v1/chats/{chatID}/messages` | v4.1.294 |
| `PUT` | `/v1/chats/{chatID}/messages/{messageID}` | v4.2.499 |
| `POST/DELETE` | `/v1/chats/{chatID}/messages/{messageID}/reactions` | v4.2.557 |

### Search (2)

| Method | Endpoint | Added |
|--------|----------|-------|
| `GET` | `/v1/search` | v4.1.294 |
| `GET` | `/v1/search/users` | v4.1.294 |

### Assets (3)

| Method | Endpoint | Added |
|--------|----------|-------|
| `POST` | `/v1/assets/upload` | v4.2.499 |
| `POST` | `/v1/assets/upload/base64` | v4.2.499 |
| `GET` | `/v1/assets/serve` | v4.2.509 |

### WebSocket (1)

| Method | Endpoint | Added |
|--------|----------|-------|
| `GET` | `/v1/ws` | v4.2.557 |

### MCP (1)

| Method | Endpoint | Added |
|--------|----------|-------|
| `POST` | `/v0/mcp` | Pre-v4.1.294 |

### App Control (1)

| Method | Endpoint | Added |
|--------|----------|-------|
| `POST` | `/v1/open` | v4.1.294 |

## Growth Rate

```
v4.1.294 (Oct 2025):  ~12 endpoints  (REST launch)
v4.2.499 (Jan 2026):  +3 endpoints   (editing, uploads)
v4.2.509 (Jan 2026):  +1 endpoint    (asset serving)
v4.2.557 (Feb 2026):  +6 endpoints   (WS, reactions, discovery)
                       ─────────────
Total:                  21 endpoints   (+75% growth in 4 months)
```

## Upcoming (Confirmed but Undocumented)

| Feature | Source | Expected |
|---------|--------|----------|
| Send-later API | batuhan, Feb 2026 | Unknown |
| Webhook events | batuhan, Dec 2025 | With headless mode |
| AI Chats API | batuhan, Mar 2026 | Very soon |
| Translation API | batuhan, Mar 2026 | Unknown |

## Authentication Evolution

| Period | Method |
|--------|--------|
| Early 2025 | Manual token creation only |
| Sep 2025 | OAuth 2.0 with PKCE added |
| Feb 2026 | Token introspection added |

Current methods:
- **OAuth 2.0 with PKCE** -- automatic for most MCP clients
- **Bearer token** -- manual creation via Settings > Developers
- **Token introspection** -- `POST /oauth/introspect`
