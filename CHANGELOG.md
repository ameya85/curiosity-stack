# Changelog

All notable changes to the Curiosity Stack plugin are documented here.

---

## [3.2.3] — 2026-03-22

### Fixed — Scenario library UX
- **Start decomposition fires directly** — sendPrompt() is now the
  primary action. Clicking "Start decomposition" sends the topic
  directly into the chat. No copying, no pasting.
- **Fallback with clear feedback** — if sendPrompt() is unavailable,
  the button shows "✓ Prompt copied — paste into chat" for 3 seconds
  so the user knows it worked.
- **Removed "Copy prompt" as primary label** — button always says
  "Start decomposition →". Copy behaviour is fallback only.
- **Manual copy box** — if clipboard API also fails, a pre-filled
  textarea appears for manual selection and copy.

---

## [3.2.2] — 2026-03-22

### Fixed — Adoption and launch experience
- **Welcome agent rewritten** — scenario library now renders automatically
  on first launch as an interactive card grid. User clicks a topic and
  the decomposition starts immediately. No commands needed on first session.
- **Progressive disclosure** — commands no longer shown upfront. Each
  feature surfaces contextually after relevant outputs:
  - India Proxy Agent prompt appears after L5
  - Save / Watchlist / Research Brief options appear after full decomposition
  - Library prompt appears after 3+ sessions
- **Setup is now optional** — first session works with defaults.
  Setup prompt offered but never blocks the experience.
- **Framework skill updated** — activates on any topic description,
  not just explicit commands. Renders layer cards progressively.
  Mini summary cards after L2 and L4.

---

## [3.2.1] — 2026-03-21

### Added
- **Scenario Library** (`skills/scenario-library/SKILL.md`) — 18 pre-built decomposition topics across 6 categories. Solves the blank slate problem for new users. Interactive HTML card browser with search, category filter, preview panel (shows all 6 layer previews before committing), and one-click launch into the full decomposition flow.
- **`/curiosity-stack:scenarios`** command — launches the scenario browser
- **Welcome message updated** — "Not sure what to decompose first? → /curiosity-stack:scenarios"

### Categories (16 scenarios total)
- 🇮🇳 Indian Business Sectors: Semiconductor packaging, Defence manufacturing, GCC opportunity, Pharma API
- 🌍 Geopolitics: Middle East → oil, Russia-Ukraine → energy, US-China tariffs, Taiwan risk
- 🌐 Global Trends: Grid-scale battery storage, Green hydrogen
- 🤖 AI — Global: AI inference demand, AI data centre infrastructure
- 🤖 AI — India: Indian IT services in AI era, India AI data annotation
- 🔒 Cybersecurity: Enterprise cyber demand, OT security

### Changed
- `plugin.json` — version bumped to 3.2.1
- `agents/welcome.md` — scenario library CTA added

---

## [3.2.0] — 2026-03-20

### Added
- **Shareable output card** — generated after every Value Chain / Mindmap. Formatted for X and LinkedIn. `#CuriosityStack` tag baked in. Warm white design, teal accent, clean typography.
- **Community signal** — `#CuriosityStack` hashtag on every card. Trackable via X search.
- **Feedback — first session** — fires once after first decomposition. Google Form link.
- **Feedback — every session** — after every output. 👍 👎 💬 + Google Form link.
- **Public share option** — after every output, option to publish as public artifact with full branding and install link.
- **Progressive layer cards** — mini visual summary card generated after L2, L4, and L6. Three natural pause points during the conversation. Individually shareable.
- **Research Brief (Option 4)** — 1-page HTML/PDF output. Executive summary, value chain snapshot, key companies, core assumption, 3 things to watch. Branded. Forwardable.
- **Animated Value Chain** — layer-by-layer build animation. Each layer slides in from left. Company nodes fade in. India proxies pulse on entrance.
- **Animated Thesis Stress Test** — three-column visual layout. Proponents left, critics right, core assumption centre. Animated entrance.
- **Invisible source attribution** — HTML comment block in every generated artifact. Plugin name, GitHub URL, author, version. Survives copy-paste.
- **Visible quality badge** — `⬡ Curiosity Stack` badge on every visual output. Designed as quality mark not watermark.
- **Branding on all outputs** — plugin name, author, `#CuriosityStack`, Substack URL, Cowork deep link on every artifact without exception.
- **`session_count` tracking** — increments in local.md after every session. Used for feedback timing.

### Changed
- **`skills/output-generator/SKILL.md`** — complete rewrite. New design system (warm white palette, 14px minimum text, A/A+/A++ toggle). Four output options (added Research Brief). Attribution badge and invisible source comment on all outputs. Full feedback flow. Public share option. Shareable card generation.
- **`skills/curiosity-framework/SKILL.md`** — progressive layer cards after L2, L4, L6. Research Brief added to output choice. `text_size` and `session_count` read from local.md.
- **`skills/thesis-stress-test/SKILL.md`** — complete visual redesign. Three-column animated layout. New design system. Attribution badge and footer.
- **`skills/watchlist-tracker/SKILL.md`** — local.md write constraint documented. Plugin now generates exact YAML block for user to paste. Attribution in digest. Cowork deep link in every email.
- **`curiosity-stack.local.md`** — new fields: `text_size`, `session_count`.
- **`plugin.json`** — version bumped to 3.2.0.

### UI Design System (new — applies to all visual outputs)
- Background: `#fafaf8` (warm white)
- Primary text: `#2c2c2c` (soft charcoal)
- Accent: `#1b5e52` (deep teal, used sparingly)
- Body text minimum: 14px
- Layer labels minimum: 16px
- Company names minimum: 13px
- Text size control: A / A+ / A++ toggle on every visual
- No gradients, no neon, no dark drama

---

## [3.1.0] — 2026-03-15

### Added
- **Decomposition Library** (`skills/decomposition-library/SKILL.md`) — saves every completed decomposition as a structured local file in `library/`. Topic, date, all 6 layer summaries, sources cited, tags, conviction placeholder. Retrieval: plugin checks library at start of new decomposition and asks if user wants to load a past session on the same topic. Optional mirror to Google Drive or Notion.
- **`/curiosity-stack:library`** command — browse, search, open, and delete saved decompositions
- **Watchlist Tracker + Trigger Alerts** (`skills/watchlist-tracker/SKILL.md`) — scheduled monitoring agent. Runs on user-set cadence (daily / weekly / fortnightly). Monitors all watchlist topics for news, regulatory changes, new entrants, and funding. Maps findings to value chain layers. Scores materiality HIGH / MEDIUM / LOW with reasoning. Trigger alerts fire when specific layer conditions are met.
- **Watchlist Agent** (`agents/watchlist-agent.md`) — autonomous agent powering the tracker. Uses web_search and web_fetch. Checks cadence before running. Delivers digest via Gmail (default) and surfaces summary in Cowork.
- **Email digest delivery** — watchlist digest sent directly to user's Gmail on cadence. Subject line prefixed with 🚨 if triggers fired. Includes Cowork deep link.
- **`/curiosity-stack:watchlist`** command — manage watchlist topics, set triggers, configure cadence and email settings
- **Source Credibility** (`skills/source-credibility/SKILL.md`) — personal source registry. Tracks which publications, databases, and analysts are cited at which layer and sector. Post-session rating prompt (max 3 sources, 60 seconds). Plugin-suggested ratings based on usage patterns after 5+ decompositions. Surfaces top-rated sources at L1 and L5 automatically.
- **`library/` folder** — local storage for decomposition files. Includes README.md placeholder.
- **Setup extended** — three new sections (Steps 6-8): decomposition library preferences, watchlist monitoring configuration, source credibility settings.
- **`curiosity-stack.local.md` extended** — new fields for library, watchlist monitoring, and source credibility.

### Changed
- `skills/setup/SKILL.md` — extended from 7 steps to 9 steps with new configuration sections
- `curiosity-stack.local.md` — full template rewrite with all new fields, organised by section
- `plugin.json` — version bumped to 3.1.0, homepage updated to announcement post URL

---

## [3.0.0] — 2026-03-13

### Added
- **Autonomous India Proxy Agent** (`agents/india-proxy-agent.md`) — `/curiosity-stack:india-proxy` now runs a full autonomous research sequence: searches Tracxn, Inc42, Screener.in, and NASSCOM, validates candidates against red flag criteria, and returns a structured shortlist with proxy pattern, access method, validation signals, and watch triggers
- **SEBI Disclaimer Hook** (`hooks/hooks.json`) — automatically appends full SEBI disclaimer to every research output at the `Stop` event; cannot be suppressed
- **`curiosity-stack.local.md`** — personal context file; users fill it once and the plugin reads it on every session; covers context, geography, themes, watchlist, sectors to deprioritise, output preference, and free-text notes
- **Customisation section in README** — three customisation paths documented: local.md editing, skill file editing, and adding custom skills
- **`CHANGELOG.md`** — this file
- **`LICENSE`** — MIT

### Changed
- `curiosity-framework/SKILL.md` — session flow now starts with Step 0: silently read `local.md` and apply user context before intake
- `company-discovery/SKILL.md` — India proxy patterns now framed explicitly as research directions with category examples; no specific company names as illustrative examples
- `sebi-compliance/SKILL.md` — added "Naming Companies — Framing Rules" section with explicit required and forbidden language when surfacing company names at Layer 5
- `commands/india-proxy.md` — updated to route to the autonomous agent
- `plugin.json` — version bumped to 3.0.0
- README — full rewrite including plugin structure diagram, agent description, local.md documentation, and "Making It Yours" section

---

## [2.0.1] — 2026-03-12

### Changed
- Removed all specific company and stock name references from public-facing files (one-pager, README, X thread, Substack post)
- Retained India proxy pattern examples in skill files with neutral category framing
- SEBI compliance language hardened throughout

---

## [2.0.0] — 2026-03-12

### Added
- SEBI compliance skill (`skills/sebi-compliance/`) — always-active, highest priority; covers hard decline triggers, language substitutions, and named company framing rules
- Thesis Stress Test skill (`skills/thesis-stress-test/`) and command (`/curiosity-stack:stress-test`)
- Reading list skill (`skills/reading-list/`) — 5 curated recommendations per decomposition
- Output choice flow — user selects Value Chain / Mindmap / Research Note after decomposition; never auto-generates all three
- MCP connectors expanded to 17

### Changed
- `india-proxy` output choice renamed from "India Proxy" to "india-proxy" for command consistency
- "Bull vs Bear" framing renamed to "Thesis Stress Test" throughout
- Author bio simplified to Substack + X only

---

## [1.0.0] — 2026-03-11

### Initial release
- Six-layer Curiosity Stack framework
- Four commands: setup, decompose, india-proxy, mindmap
- Eight skills: curiosity-framework, setup, company-discovery, output-generator, source-guide, reading-list, sebi-compliance, thesis-stress-test
- MCP connectors: Google Drive, Gmail, Notion
