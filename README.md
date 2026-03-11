# 🌉 SETU Protocol

### System of Extensible & Tangible User Interfaces

**An open protocol for AI agents to discover, assemble, and render trusted UI components from a decentralised provider marketplace — based on user intent.**

[![Status](https://img.shields.io/badge/status-draft--spec-orange)](https://github.com/setu-protocol/setu)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue)](LICENSE)
[![Version](https://img.shields.io/badge/spec-v0.1--alpha-purple)](SPEC.md)
[![Discord](https://img.shields.io/badge/community-discord-7289da)](https://discord.gg/setu-protocol)

*Setu (सेतु) — Sanskrit/Hindi for bridge. SETU bridges user intent with trusted provider interfaces, assembled by AI agents in real time.*

---

[Why SETU](#-why-setu) · [How It Works](#-how-it-works) · [Architecture](#-architecture) · [Spec](#-specification) · [Roadmap](#-roadmap) · [Contributing](#-contributing)


---

## 🌍 Why SETU

The AI agent ecosystem has solved tool access and agent communication. It has not solved the UI layer.

| Protocol | What it solves | Scope |
|----------|---------------|-------|
| MCP | Agent ↔ Tools & Data | Single provider |
| AG-UI | Agent ↔ Frontend app | Single company |
| A2UI | Agent → UI rendering format | Single company |
| A2A | Agent ↔ Agent coordination | Cross-company |
| **SETU** | **Trusted UI provider marketplace** | **Cross-company, open** |

Today, when a user tells an AI agent *"book me a ride to the airport"*, one of two things happens:

- The agent generates a plain text response with a link
- The agent renders UI — but only within one company's walled garden

**Neither is good enough.**

The user has to leave their AI interface, open a separate app, re-authenticate, and complete the task in a fragmented experience. The AI layer and the UI layer are still disconnected.

> *"Chat window is not the answer to everything... not everything is conversational."*
> — Industry researcher, ACM DIS 2025

SETU fixes this. It is the missing bridge between the agent stack and the provider UI ecosystem.

---

## 💡 How It Works

SETU enables a new interaction paradigm in three steps:

### 1. User expresses intent
```
User → AI Agent: "Book me a ride to the airport at 6pm"
```

### 2. Agent queries the SETU registry
```json
{
  "intent": "ride_booking",
  "context": {
    "destination": "airport",
    "time": "18:00+1d",
    "location": "user_current"
  },
  "trust_tier": "verified"
}
```

### 3. SETU returns trusted provider UI components — rendered inline
```
Agent renders → [ Uber UI brick ] [ Lyft UI brick ] [ Ola UI brick ]
                  side by side, inside the agent interface
                  user selects, transacts, confirms — without leaving
```

No app switching. No re-authentication. No fragmented experience.

---

## 🏗 Architecture

SETU is a four-layer protocol stack:

```
┌─────────────────────────────────────────────┐
│              L1 — INTENT LAYER              │
│   Parses user intent into structured query  │
│   { capability, context, geography, prefs } │
├─────────────────────────────────────────────┤
│             L2 — REGISTRY LAYER             │
│   Decentralised provider marketplace        │
│   Manifests · Trust scores · Capabilities   │
├─────────────────────────────────────────────┤
│              L3 — RENDER LAYER              │
│   Wire protocol for UI component delivery   │
│   Builds on AG-UI / A2UI standards          │
├─────────────────────────────────────────────┤
│           L4 — TRANSACTION LAYER            │
│   Routes user actions back to providers     │
│   Logs revenue events · Handles auth        │
└─────────────────────────────────────────────┘
```

### Provider Component Manifest

When a company registers a UI brick in SETU, they submit a manifest:

```json
{
  "provider_id": "did:setu:uber-technologies",
  "name": "Uber Ride Booking",
  "capabilities": ["ride_booking", "ride_tracking", "fare_estimate"],
  "ui_endpoint": "https://setu.uber.com/components/ride-booking",
  "render_format": "react_component",
  "geographies": ["IN", "US", "GB", "AU"],
  "trust_tier": "verified",
  "transaction_fee": 0.02,
  "data_schema": {
    "requires": ["user_location", "destination"],
    "retention": "session_only"
  }
}
```

### Trust Tiers

SETU enforces a trust framework across all registered providers:

| Tier | Requirements | Badge |
|------|-------------|-------|
| **Verified** | Identity verified, SOC2 compliant, SLA > 99.5% | 🟢 |
| **Registered** | Identity verified, basic compliance | 🟡 |
| **Community** | Open source, unverified | 🔵 |

Agents can filter by trust tier based on the sensitivity of the user's request.

---

## 📐 Specification

The full SETU specification is in [`SPEC.md`](SPEC.md). Key sections:

- [Intent Schema](SPEC.md#intent-schema) — how agents query the registry
- [Provider Manifest](SPEC.md#provider-manifest) — how providers register UI components
- [Render Protocol](SPEC.md#render-protocol) — how components are transmitted and rendered
- [Transaction Protocol](SPEC.md#transaction-protocol) — how user actions are routed back
- [Trust Framework](SPEC.md#trust-framework) — how providers are verified and scored

> **SETU v0.1 is a draft specification.** We are actively seeking feedback from the developer community, AI agent builders, and UI providers before v1.0 is finalised.

---

## 🗺 Roadmap

### Phase 1 — Spec & Ecosystem *(Now — Month 6)*
- [x] Draft SETU v0.1 specification
- [ ] Reference implementation: registry + demo agent + 3 sample provider bricks
- [ ] Developer documentation
- [ ] arXiv position paper
- [ ] Neutral governance — Linux Foundation / Apache application
- [ ] First 3 anchor provider integrations

### Phase 2 — Consumer Proof *(Month 6–12)*
- [ ] SETU-powered consumer demo: ride, food, streaming — all inline in one agent
- [ ] Auto-adapter layer: convert existing REST APIs into SETU-compliant bricks
- [ ] First 100 provider integrations
- [ ] Transaction revenue share — first monetisation signal

### Phase 3 — Decentralise & Scale *(Month 12–24)*
- [ ] Transition registry to decentralised architecture
- [ ] Enterprise tier: private SETU registries for internal tools
- [ ] Agent framework integrations: LangGraph, AutoGen, CrewAI, Goose
- [ ] Approach major AI vendors for standard adoption

---

## 🔬 Research Foundation

SETU is grounded in emerging research on generative UI and agentic systems:

- **Nielsen Norman Group (2025)** — GenUI is moving from theory to practice; simple interactive elements are beginning to appear contextually within AI conversations
- **ACM DIS 2025** — Formal definition of GenUI; industry caution against defaulting to chat for all interactions
- **Google Research (2025)** — Human raters strongly prefer generative UI over standard LLM text outputs; early days of fully AI-generated user experiences
- **AG-UI Protocol (2025)** — Standardises agent-to-frontend connections; SETU builds the marketplace layer above this
- **Google A2UI (Dec 2025)** — Solves cross-platform UI rendering; SETU adopts this as its render wire format
- **MCP-UI / Goose (2025)** — Proves MCP servers can return interactive UI; adoption at scale is the unsolved problem SETU addresses

---

## 🤝 Contributing

SETU is an open protocol. We need:

- **Protocol designers** — help refine the spec
- **AI agent builders** — integrate SETU into your agent framework
- **UI providers** — register your first component brick
- **Security researchers** — stress test the trust framework
- **Developer advocates** — help grow the community

### How to contribute

1. Read the [Specification](SPEC.md)
2. Open an [Issue](https://github.com/setu-protocol/setu/issues) with your feedback
3. Join the [Discord](https://discord.gg/setu-protocol) — introduce yourself in `#introductions`
4. Submit a PR against the spec — all changes go through community review

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for full guidelines.

---

## 📄 License

SETU Protocol Specification is published under the **Apache License 2.0**.

This means you can use, modify, and distribute the spec freely — including in commercial products — as long as you include attribution. The protocol is and will remain open.

---

## 🌉 The Name

*Setu (सेतु)* is the Sanskrit and Hindi word for **bridge**.

In Indian mythology, Ram Setu was the bridge built to connect two worlds — assembled piece by piece, by many hands, with a singular purpose.

SETU the protocol is that bridge — connecting user intent to provider interfaces, assembled piece by piece from trusted UI components, by AI agents acting on your behalf.

---

**SETU is an open protocol. No single company owns it. Everyone can build on it.**

*Built with ♥ and a conviction that the UI layer of the agentic web should be open.*

[spec](SPEC.md) · [discord](https://discord.gg/setu-protocol) · [contribute](CONTRIBUTING.md) · [twitter/x](https://x.com/setuprotocol)
