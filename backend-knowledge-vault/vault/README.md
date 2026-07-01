# Backend Engineering Knowledge Vault (Obsidian)

A fully cross-linked Obsidian vault covering distributed systems, microservices, messaging, databases, caching, Kubernetes, system design, and low-level design.

## How to open
1. Install Obsidian (free).
2. Open Obsidian → **Open folder as vault** → select this folder.
3. Open **🗺️ MOCs/00 - Home** — that's your dashboard.
4. Press **Ctrl/Cmd + G** for the Graph View (colours are pre-configured per topic).

## Structure
- **🗺️ MOCs/** — Maps of Content (navigation hubs). Start at `00 - Home`.
- **📝 Concepts/** — atomic concept notes (one idea each).
- **🧩 Patterns/** — microservice & resilience patterns.
- **🏛️ System Designs/** — end-to-end designs that link the concepts they use.
- **💻 LLD Problems/** — OO design problems.
- **📂 Templates/** — note templates (Settings → Templates folder is preset).

## What makes the graph work
- Every note ends with a **🔗 Connections** block of `[[wikilinks]]`.
- Cross-cutting concepts (Idempotency, Retry, Circuit Breaker, Sharding...) link many sections.
- Tags (`#kafka`, `#reliability`, ...) colour and filter the graph.
- Validated: zero broken links, zero orphan notes.

## Adding your own notes
Use a template (Cmd+P → "Insert template"), write the idea, and link it with `[[...]]`. It joins the graph automatically.
