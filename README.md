# Cascadia Airways · System Operations Copilot Demo

A self-contained, single-file interactive demo showing how **Microsoft 365 Copilot**, **Copilot Studio**, **Power Platform**, and **Microsoft Foundry** map onto six airline-operations use cases for a fictional mid-size carrier, Cascadia Airways (hub: KSEA).

> Cascadia Airways, its flight numbers (CAS-prefixed), crew/passenger names, gates, tail numbers, and operational data are all fictional. The demo is intended for sales conversations, architecture discussions, and workshop framing.

## The premise

When something goes wrong at an airport — weather, mechanical, ATC flow, medical divert, crew timeout — the cascade across the network is bigger than a single analyst can hold in their head. Downstream flights, crew legality, connecting passengers, gate conflicts, curfews, fuel, maintenance slots all ripple at the same time. Even when nothing goes wrong, every gate has optimizations an AI can surface in real time that a human would not catch before off-block.

This demo shows how a M365 Copilot + Copilot Studio + Foundry stack can both **run the disruption cascade** and **make every gate a little more productive every day**.

## The four-layer Microsoft AI stack

| Layer | Product | Role |
|---|---|---|
| 1 | Microsoft 365 Copilot | Productivity layer for Dispatchers, station coordinators, and ops leadership — Outlook, Teams, Word, Excel, PowerPoint, OneDrive |
| 2 | Copilot Studio | Conversational agent layer — six Cascadia agents |
| 3 | Power Platform | Workflow, app, and ops-management layer — Power Apps, Automate, Pages, Dataverse |
| 4 | Microsoft Foundry | Advanced AI orchestration, evaluation, and governance — the spine for the IROps Cascade Commander and Predictive Maintenance agents |

## Six use cases covered

1. **IROps Cascade Commander (UC1)** — When a disruption hits (wx, ATC, mechanical, medical divert), simulates the network ripple across downstream flights, crew legality, gates, curfews, and MX. Recommends three ranked recovery plans within 90 seconds.
2. **Gate Turnaround Optimizer (UC2)** — Takes the **handwritten** or scanned ramp turn sheet + fuel slip, OCRs them, cross-checks Sabre AirOps, and drafts a predicted-off-block turn plan on Cascadia letterhead ready for the gate supervisor to sign.
3. **Predictive Maintenance Copilot (UC3)** — Ingests ACARS sensor anomalies, predicts component failure probability, reserves an MX slot, and pre-orders parts before an AOG happens.
4. **Crew Legality & Reassignment Agent (UC4)** — Monitors every crew pairing against FAR 117 duty/rest. During IROps, proactively proposes reassignments (reserve call-outs, deadhead swaps) to keep aircraft moving without tripping legality.
5. **Passenger Disruption Comms & Rebook (UC5)** — Drafts EU261 / DOT tarmac-rule compliant rebook + compensation messaging, tone-calibrated for medical, military, UMNR, and VIP passengers. English + Spanish, approval-gated before send.
6. **Baggage Misconnect Orchestrator (UC6)** — Predicts short-connect bag risk for every inbound, proposes priority offload sequence, short-ship vs. hold decisions, and auto-generates BT/WT paperwork when bags miss.

## Highlighted demo canvases

Both canvases are live-interactive — click through the home app grid:

- **"Turn Plan Intake" tile** → Gate Turnaround: a scanned, handwritten ramp turn sheet appears on the left; Copilot's OCR extraction + Sabre AirOps cross-check runs on the right; the auto-drafted Gate Turn Plan populates below on Cascadia letterhead. Click **Approve & File to Sabre** to see the dispatch receipt + gate off-block event.
- **"Word" tile** → IROps Cascade view: the active disruption at KORD is shown with the predicted network ripple, three recovery options ranked by pax impact and crew legality, and a batch of passenger comms queued for approval.

## Four personas

- **Sarah Chen, Senior Dispatcher (SOC)** — network ops, sees IROps Cascade + Turn Plan Intake + Crew Legality + Pax Comms.
- **Marcus Johnson, VP System Operations** — exec triage: cumulative pax impact, media-sensitive diversions, DOT SLA, board readout.
- **Maria Gutierrez, Station Operations Coordinator (SEA)** — station view: gate turn sheets queued, short-connect bags, station-level pax comms.
- **Dan Kowalski, IT Director** — governance view: ACARS → Azure data flow, EU261 SLA monitor, recovery-decision audit, DOT complaint volume.

## Running locally

Just open `index.html` in a modern browser. No build step, no external dependencies.

## Known rebrand residuals

The demo was rebranded from a sibling legal-ops demo template. A small number of narrative strings in deep inbox/case-detail views still contain legacy-domain lexicon (e.g., some witness-statement paragraphs on the discovery canvas). These are on the to-do list; the top-level home, personas, agent tiles, and primary canvases have been retargeted for airline operations.
