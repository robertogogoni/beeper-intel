# Beeper Ecosystem Map

> A complete visualization of how Beeper's components interconnect: Desktop API, SDKs, bridges, MCP, AI agents, and community tools.

## Master Ecosystem Diagram

```mermaid
graph TB
    subgraph core["Beeper Core"]
        BD["Beeper Desktop"]
        BA["Beeper Android"]
        BI["Beeper iOS"]
    end

    subgraph api["Desktop API Layer"]
        DAPI["Desktop API<br/>(REST /v1)"]
        OAPI["OpenAPI Spec"]
        MCP_EP["MCP Endpoint<br/>(/v0/mcp)"]
        WS["WebSocket<br/>(/v1/ws)"]
    end

    subgraph sdks["Official SDKs (Stainless-generated)"]
        TS["TypeScript SDK<br/>v4.5.0"]
        PY["Python SDK<br/>v4.1.296"]
        GO["Go SDK<br/>v0.4.0"]
        CLI["CLI Tool<br/>v0.2.0"]
        PHP["PHP SDK"]
        SQL["SQL SDK<br/>(experimental)"]
    end

    subgraph mcp_clients["MCP Clients"]
        CD["Claude Desktop"]
        CC["Claude Code"]
        CUR["Cursor"]
        VSC["VS Code"]
        RAY["Raycast"]
        WARP["Warp"]
        CDX["Codex"]
        GEM["Gemini CLI"]
        WIND["Windsurf"]
    end

    subgraph bridges["Bridge Ecosystem"]
        BM["bridge-manager<br/>(bbctl)"]
        subgraph official_bridges["Official (mautrix)"]
            WA["WhatsApp"]
            TG["Telegram"]
            SIG["Signal"]
            META["Facebook/Instagram"]
            DISC["Discord"]
            SLACK["Slack"]
            LI["LinkedIn"]
            GMSGS["Google Messages"]
            GCHAT["Google Chat"]
            IMSG["iMessage"]
            TW["X / Twitter"]
            GV["Google Voice"]
            BS["Bluesky"]
        end
        subgraph community_bridges["Community Bridges"]
            IRC["IRC (Heisenbridge)"]
            LINE["LINE"]
            SNAP["Snapchat"]
            ZALO["Zalo"]
            IMSG2["iMessage v2 (Rust)"]
        end
    end

    subgraph agents["AgentRemote"]
        AR["agentremote"]
        AI_BR["AI Bridge"]
        CODEX_BR["Codex Bridge"]
        OC_BR["OpenClaw Bridge"]
        OCODE_BR["OpenCode Bridge"]
    end

    subgraph community["Community Tools"]
        DOCKER["docker-beeper<br/>(56 stars)"]
        BEEPCTL["beepctl<br/>(30 stars)"]
        BPCLI["beeper-cli<br/>(25 stars)"]
        THEMES["themes<br/>(156 stars)"]
        METRO["Metrology<br/>(41 stars)"]
    end

    BD --> DAPI
    BD --> MCP_EP
    BD --> WS
    OAPI --> TS & PY & GO & CLI & PHP & SQL

    DAPI --> TS & PY & GO & CLI & PHP & SQL

    MCP_EP --> CD & CC & CUR & VSC & RAY & WARP & CDX & GEM & WIND

    BM --> official_bridges
    BM --> community_bridges

    AR --> AI_BR & CODEX_BR & OC_BR & OCODE_BR

    BD -.-> BM
    BD -.-> AR

    TS --> BEEPCTL
    DAPI --> DOCKER
    DAPI --> BPCLI
    BD -.-> THEMES & METRO

    BA --> MCP_AND["mcp-android"]
    MCP_AND --> GEM

    style core fill:#1a1b27,color:#a9b1d6,stroke:#7aa2f7
    style api fill:#1a1b27,color:#a9b1d6,stroke:#bb9af7
    style sdks fill:#1a1b27,color:#a9b1d6,stroke:#7dcfff
    style mcp_clients fill:#1a1b27,color:#a9b1d6,stroke:#9ece6a
    style bridges fill:#1a1b27,color:#a9b1d6,stroke:#ff9e64
    style agents fill:#1a1b27,color:#a9b1d6,stroke:#f7768e
    style community fill:#1a1b27,color:#a9b1d6,stroke:#e0af68
```

## SDK Generation Pipeline

```mermaid
flowchart LR
    SPEC["OpenAPI Spec<br/>(desktop-api-openapi)"] --> STAINLESS["Stainless<br/>(Auto-generator)"]
    STAINLESS --> JS["@beeper/desktop-api<br/>TypeScript v4.5.0"]
    STAINLESS --> PY["Python v4.1.296"]
    STAINLESS --> GO_SDK["Go v0.4.0"]
    STAINLESS --> CLI_SDK["CLI v0.2.0"]
    STAINLESS --> PHP_SDK["PHP"]
    STAINLESS --> SQL_SDK["PLpgSQL"]

    style SPEC fill:#bb9af7,color:#1a1b27
    style STAINLESS fill:#7aa2f7,color:#1a1b27
```

## Bridge Architecture

```mermaid
flowchart TB
    USER["User Device"] --> BD["Beeper Desktop"]
    BD --> HS["hungryserv<br/>(Matrix homeserver)"]

    HS <--> BM["bridge-manager<br/>(bbctl)"]

    BM --> WA["mautrix/whatsapp"]
    BM --> TG["mautrix/telegram"]
    BM --> SIG["mautrix/signal"]
    BM --> META_BR["mautrix/meta<br/>(FB + IG)"]
    BM --> DISC_BR["mautrix/discord"]
    BM --> SLACK_BR["mautrix/slack"]

    WA --> WA_NET["WhatsApp Network"]
    TG --> TG_NET["Telegram Network"]
    SIG --> SIG_NET["Signal Network"]
    META_BR --> FB_NET["Facebook / Instagram"]
    DISC_BR --> DISC_NET["Discord"]
    SLACK_BR --> SLACK_NET["Slack"]

    style USER fill:#7aa2f7,color:#1a1b27
    style BD fill:#bb9af7,color:#1a1b27
    style HS fill:#f7768e,color:#1a1b27
    style BM fill:#9ece6a,color:#1a1b27
```

## MCP Data Flow

```mermaid
sequenceDiagram
    participant User as User (in IDE)
    participant Client as MCP Client
    participant Beeper as Beeper Desktop
    participant Network as Chat Network

    User->>Client: "Find messages from John about dinner"
    Client->>Beeper: POST /v0/mcp (search_messages)
    Beeper->>Beeper: Local search (encrypted data)
    Beeper-->>Client: Results (Markdown format)
    Client-->>User: "Found 3 messages..."

    User->>Client: "Send reply: I'll be there at 7"
    Client->>Beeper: POST /v0/mcp (send_message)
    Beeper->>Network: Send via bridge
    Network-->>Beeper: Delivery confirmation
    Beeper-->>Client: Success
    Client-->>User: "Message sent"
```

## Component Count Summary

| Category | Count | Notes |
|----------|-------|-------|
| Official repos | 125 | 8 archived, 92 active |
| Community repos | 35+ | CLI tools, themes, bridges, MCP servers |
| Official SDKs | 6 | All Stainless-generated |
| MCP clients supported | 9 | Claude, Cursor, VS Code, Raycast, Warp, etc. |
| Official bridges | 13 | via mautrix |
| Community bridges | 5+ | IRC, LINE, Snapchat, Zalo, iMessage v2 |
| AI agent bridges | 4 | Codex, OpenClaw, OpenCode, generic AI |
| API endpoints | 21 | REST /v1 |
| MCP tools | 10 | search, list, send, archive, etc. |

## Cross-References

- [AgentRemote Analysis](agentremote-analysis.md) -- deep dive on the AI agent platform
- [Bridge Landscape](bridge-landscape.md) -- complete bridge listing
- [Community Intelligence](community-intelligence.md) -- developer ecosystem insights
