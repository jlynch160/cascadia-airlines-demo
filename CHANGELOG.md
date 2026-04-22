# Changelog

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
