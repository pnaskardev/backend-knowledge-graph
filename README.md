# Backend Engineering Knowledge Vault (Obsidian)

A cross-linked Obsidian vault for **SDE-1 / SDE-2 system-design interview prep**, organized as an ordered curriculum: distributed systems, databases, caching, messaging, microservices, Kubernetes, low-level design, and end-to-end system designs.

## How to open
1. Install Obsidian (free).
2. Open Obsidian → **Open folder as vault** → select this folder.
3. Open **`00 - Start Here/STUDY_PLAN`** — the ordered "what to study after what" checklist. (Or `00 - Home` for the dashboard.)
4. Press **Ctrl/Cmd + G** for the Graph View.

## Structure (folders are numbered in study order)
- **00 - Start Here/** — `STUDY_PLAN` (the curriculum), `00 - Home`, and the study method (`How to study fast`, `How to Drill`).
- **01 - Web & Networking/** — API design, load balancing, CDN, auth.
- **02 - Databases/** → **03 - Caching/** → **04 - Distributed Systems/** → **05 - Scaling & Data Distribution/**
- **06 - Messaging & Streaming/** → **07 - Microservices & Resilience/** → **08 - Kubernetes & Deployment/**
- **09 - Low Level Design/** — SOLID, design patterns, classic OO problems.
- **10 - System Design Case Studies/** — end-to-end designs (do these last).
- **_archive/Templates/** — the old note templates, kept for reference (not part of the workflow).

Each domain folder also contains its own **MOC** (Map of Content) hub note.

## How the notes work
- Every topic is a **blank canvas** — you fill it in your own words (definition, why, key trade-off, one recall question). A topic can grow into a full article whenever you like; there's no required template.
- Each note ends with a **🔗 Connections** block of `[[wikilinks]]` — these power the Graph View and let you navigate by relationship.
- Tags: keep `#review` while learning, switch to `#solid` once you can explain a topic out loud without looking.

## Adding your own notes
Create a note anywhere, write the idea, and link it with `[[double brackets]]`. It joins the graph automatically. Obsidian uses shortest-path link resolution, so links work regardless of which folder a note lives in.
