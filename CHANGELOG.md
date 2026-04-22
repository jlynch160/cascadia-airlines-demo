# Changelog

## 2026-04-22 — IROps Cascade Commander canvas (marquee airline UC)

Built the centerpiece interactive canvas that hits the "cascading-disruption + gate-productivity" brief head-on.

### New home tile + app-shell
- **"IROps Cascade" tile** on the home grid (all four personas), rendered with a custom ripple-wave logomark (concentric orange arcs fanning into teal dots) and a red-orange `LIVE` badge with the pulse-halo animation.
- **`#app-irops` app-shell canvas** (~360 lines of HTML + 220 lines of scoped CSS + 130 lines of JS) routes from the tile via the existing `openApp('irops')` pipeline.

### Three-column live dashboard

**Top command bar** — title + subtitle ("grounded on live Sabre AirOps + FAA SWIM + METAR/TAF"), a live ticking clock chip (fictional start 06:47 PT, advances in real time while the canvas is open), `Simulate cascade` CTA, and `Ask Copilot`.

**Active-event banner** — pulsing `GROUND STOP` severity badge, KORD event headline with real aviation metadata (AFP ZAU03, EDCT, KMDW/KMKE/KRFD alternates), and four KPI tiles (47 flights affected · 6,284 pax exposed · 2 FAR 117 risks · $312K DOT exposure).

**Left column — Network ripple viz** — the "what a human analyst would miss" story. Red origin node (ORD · Ground Stop) trunk with four categorized branches:
- Downstream flight delays (23 flights, with real CAS flight numbers, tails, STDs, and predicted delays)
- Crew legality risk (2 FAR 117 pairings with FDP cushion math)
- Passenger connections at risk (1,842 pax · 14 UMNRs · 6 WCHR · 2 medical · DOT 2h tarmac trigger analysis)
- Gate + ramp conflicts (SEA B12/B17/C3/C7 · MDW capacity at 11:00 · curfew risk on CAS2118 ICN inbound)

**Middle column — Copilot recovery plans** — three ranked plan cards with a gradient-border treatment on the recommended Plan A:
- **Plan A (recommended)** — Route around ORD via MDW: tail swap N8421CA↔N6152CA, deadhead FO Martinez, cancel CAS1318, $146K, 81% on-time, all FAR 117 legal, $0 DOT.
- **Plan B (conservative)** — Hold SEA: cheap ($38K) but $312K DOT exposure, 22% on-time, 2 pairings at FDP risk.
- **Plan C (aggressive)** — Cancel 4 flights: clean recovery but $412K net cost (EU261 compensation for 96 EU-origin pax).

Each plan surfaces five KPIs (misconnects, crew legality, DOT exposure, net cost, on-time rate) with ok/warn/bad color coding. Accept / Modify / "Why this plan?" buttons wired — `Why this plan?` fires a 7.5 s Copilot-styled toast with the ranking rationale.

**Right column — Gate productivity (the "even when nothing's wrong" angle)** — six live gate cards for SEA hub, covering the full turn-productivity surface:
- **B12 · CAS1247**: parallelize fueling + catering (save 6 min), pre-position cabin crew (save 2 min)
- **B17 · CAS0842**: bag loader re-task, 11-min recovery on a predicted +11 delay
- **C3→C7 · CAS1102 inbound**: gate swap to free C3 for priority CAS2201 OGG→SEA
- **A4 · CAS0517**: auto-upgrade 2 loyalty pax on standby (NPS +14)
- **D11 · CAS2118 ICN→SEA**: pre-stage overnight team, pre-position bus B-4, avoid 01:00 curfew breach
- **N1 · CAS4412 SEA→YVR**: offer 4 standby pax on predicted under-load (+$1,842 revenue)

Each gate card has Apply / secondary-action chips that fire a `showToast` + flash-green `ir-applied` CSS animation on the card.

**Telemetry footer** — dark-themed live log (Foundry · GraphModel, Sabre AirOps, Crew Legality Agent, Pax Comms Agent, Pred MX Agent, Bag Misconnect Agent, Gate Optimizer, Purview). Seeds with 8 realistic entries on app-open; prepends new rows whenever Simulate Cascade runs or a gate suggestion is applied.

### Interactive behaviors

- **Simulate cascade button** runs a 7-step animated narration (0.3 s → 5.1 s) with Copilot-styled toasts at start and finish. Streams new rows into the telemetry log with realistic timing: graph rebuild → FAA SWIM pull → 128 candidate pruning → crew-legality check → pax impact → cost model → Purview labeling.
- **Accept plan A/B/C** writes an audit row to the telemetry log and fires a Copilot-styled toast naming the dispatched downstream systems (Sabre AirOps, Crew Scheduling, Pax Comms, Ramp Ops, Purview).
- **Gate "Apply" buttons** flash the card green and log to telemetry with a gate-specific outcome message ("cabin crew pre-positioned · predicted off-block 07:34").
- **Live clock** advances second-by-second while the canvas is open; the cascade-graph-age counter ticks up in parallel.

### Aviation realism checklist
- Real FAA systems named: SWIM, AFP (ZAU03), EDCT, FSDO, Part 117 §b/§c
- Real alternates for ORD: KMDW (Midway), KMKE (Milwaukee), KRFD (Rockford)
- Real regulatory concepts: FAR 117 crew duty/rest, DOT 3-hour tarmac rule (with 2h notify trigger), EU261 compensation thresholds
- Real ops concepts: pairings, FDP cushion, deadhead, tail swap, pax rebook sequencing, UMNR/WCHR/medical special-handling codes, cargo short-ship vs. hold, NPS, revenue-management standby release
- Aircraft registrations use the Cascadia `N####CA` pattern (fictional but syntactically valid)
- Flight numbers use `CAS####` with realistic route pairings (SEA-ORD, SEA-LAX, SEA-DEN, SEA-YVR, OGG-SEA, ICN-SEA, SEA-MDW)

---

## 2026-04-22 — Fork + airline rebrand (initial)

Forked from the `king-county-pao-demo` (KCPAO Microsoft 365 + Copilot demo) and rebranded for the fictional carrier **Cascadia Airways** (hub KSEA). This changelog tracks what is *shipped* in the rebrand vs. what is still on the punch list.

### What changed (shipped)

**Brand identity**
- New color palette: navy `#0b2545` + sky `#0ea5e9` + sunrise-orange `#f59e0b` + teal `#14b8a6`, replacing the legal-office navy+gold. All CSS var values updated in-place (variable names kept to avoid churn).
- New logomark: swept-delta-wing on navy roundel with orange wash and teal nose, replacing the scales-of-justice seal. Rendered as `#casaMark` SVG symbol used across splash, topbar, sign-in, favicon, and document letterhead.
- New favicon (inline SVG data URI).
- Splash title → `Cascadia Airways System Operations`. Browser tab shows the wing mark + full title.
- Sign-in: tenant email `sarah.chen@cascadia-air.com`, brand strip `CASCADIA AIRWAYS · Microsoft 365`.

**Terminology (global string replacements, 1,800+ edits across 6 passes)**
- KCPAO / King County PAO → Cascadia Airways (with CASA as the 4-letter abbrev).
- DPA / Senior DPA / Chief Deputy → Dispatcher / Senior Dispatcher / VP SysOps.
- Sheriff / KCSO / Det. → Ramp / Ramp Ops / Ramp Lead.
- Prosecutorial Governance / Prosecutor Service Delivery → Operations Governance / Operations Service Delivery.
- RCW / CrR 4.7 / Marsy's Law → FAR / FAR 117 / EU261 & DOT tarmac rule.
- Odyssey / JIS / WA File & Serve → Sabre AirOps / Sabre Crew+Ops / ARINC Direct.
- Declaration of Probable Cause → Gate Turn Authorization; Certification for Determination of Probable Cause → Certified Gate Turn Plan (CGTP).
- State v. Reyes / State v. Chang → Flight CAS1247 / Flight CAS0842.
- Bar-admission cert → ATP currency. Attorney/witness-worker data boundary → Dispatcher/crew-worker boundary.
- Tenant domains: `kingcounty.gov` / `kingcounty.onmicrosoft.com` / `kingcounty.sharepoint.com` → `cascadia-air.com` / `cascadia-air.onmicrosoft.com` / `cascadia.sharepoint.com`.

**Personas (all four rewritten)**
- Sarah Chen → Senior Dispatcher · SOC (primary: IROps Cascade + Turn Plan + Crew Legality + Pax Comms).
- Marcus Johnson → VP System Operations (primary: IROps exec view + Crew Legality + Pred MX + Regulatory Desk).
- Maria Gutierrez → Station Operations Coordinator · SEA Hub (primary: Turn Plan + Bag Misconnect + Pax Comms station view + IROps slice).
- Dan Kowalski → IT Director · Cascadia Tech Services (governance: Pred MX + Pax Comms SLA monitor + IROps audit + Regulatory Desk).

**Hero + top chrome**
- Hero rewritten with the cascade hook: "a ground stop at KORD that is rippling into 47 downstream Cascadia flights. Copilot has pre-staged three recovery options."
- Date stamp now carries a METAR snippet and the SEA-Hub tag.
- Topbar Copilot fly-out prompts retargeted: CAS1247 diversion · ORD cascade · 10:00 ops brief prep.
- App grid: "Report Intake" tile renamed to "Turn Plan Intake" with tagline "Ramp turn sheets → turn plans".
- Shifts tile retargeted: "Gate agent + ramp schedules".

**Six agents rewritten in the PERSONAS registry**
- UC1 IROps Cascade Commander — network-ripple simulation + three ranked recovery plans.
- UC2 Gate Turnaround Optimizer — handwritten ramp turn sheet → AI turn plan.
- UC3 Predictive Maintenance Copilot — ACARS anomalies → predicted AOG + MX slot booking.
- UC4 Crew Legality & Reassignment — FAR 117 duty-time monitor + proactive reassignment.
- UC5 Passenger Disruption Comms & Rebook — EU261/DOT-compliant messaging, tone-calibrated.
- UC6 Baggage Misconnect Orchestrator — short-connect risk + offload sequencing.

**Supporting assets copied from template**
- `staticwebapp.config.json`, M365 product logos (Outlook/Teams/Word/Excel/PowerPoint/OneDrive/M365), `copilot-logo.png`.

### Still on the punch list (visible "looks fake" gaps)

These deeper content blocks still contain narrative strings from the original KCPAO legal demo that a rebrand string-replace can't cleanly handle — they need scenario-rewrites:

- **Outlook seed data (lines ~10820–10900)** — email subjects/bodies still reference the overnight charging queue, a residential-burglary Ramp Lead email, and a Reyes-family victim-comms softening request. Needs: rewrite to airline scenarios (ground-stop handoff, crew-legality warning, gate-conflict escalation).
- **Sheriff Report Intake canvas / Document viewer (lines ~9175–9700)** — the handwritten form still shows a KCSO field-incident form with burglary fields; the drafted "declaration" on letterhead still has the pleading-paper legal layout. Needs: handwritten ramp turn sheet + fuel slip layout; drafted output becomes the Certified Gate Turn Plan on Cascadia letterhead.
- **Discovery Redaction / Word canvas (lines ~8049–8180)** — the 312-page packet and witness-statement page 42 still render with legal-narrative content. Needs: replace with the IROps Cascade dashboard (ground stop at KORD → ripple → recovery plan → pax comms queue).
- **Power Automate flow definitions (lines ~12441–12752)** — the two canvases (Intake + Redaction) have 13- and 12-step flows with legal-domain step names. Needs: rewrite as Turn-Plan-Intake flow + IROps-Cascade flow with airline connector steps (METAR feed, Sabre AirOps, crew legality check, pax comms fan-out).
- **Copilot Studio agent designer content (lines ~8514–8540, ~7770)** — agent overview/knowledge/topics/actions for the 6 agents. Needs: airline-specific system prompts, knowledge sources, guardrails, and KPIs.
- **PowerPoint / Copilot Pages narratives** — quarterly-review decks and collaboration pages still reference legal-domain metrics. Needs: retarget to dispatch-service-delivery metrics.
- **Admin Center / Agent 365 / Purview views** — governance dashboards still show legal-domain policy names and document types. Needs: retarget to airline equivalents.

### Implementation notes

- Six scripted sed/regex-replace passes were run and then deleted; they lived in the project folder as `rebrand.py` through `rebrand6.py` during development. Total replacements: ~1,800.
- CSS color variables kept the `--kc-*` prefix internally to minimize churn; only the hex values changed.
