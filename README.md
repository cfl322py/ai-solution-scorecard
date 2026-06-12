# AI Solution Quality & Risk Scorecard

A transparent, rule-based tool for triaging AI use cases in regulated industries. Score a use case across feasibility, evaluation rigor, risk, and responsible-by-design, then get a clear **Stop / Pivot / Proceed / Scale** verdict with the risks to watch and the guardrails that fired.

**Live demo:** https://cfl322py.github.io/ai-solution-scorecard/

---

## Why I built it

Most AI pilots in pharma stall for the same reason. Nobody scored them honestly before the build started. A use case that sounds promising in theory turns out to have no way to measure whether its outputs are sound so the work suffers, or on the other extreme it automates a decision where human judgment is still very much needed in the loop.

I wanted a simple way to ask those questions up front, in language a regulated-industry team already uses, and to get back a defensible recommendation.

## What it does

You describe a use case and answer a short set of questions. The tool returns:

- A composite quality score out of 100
- A Stop / Pivot / Proceed / Scale verdict
- A breakdown across the four dimensions
- The top risks to watch, ranked by severity
- A plain-language rationale, assembled from your answers
- Any responsible-AI guardrails that fired, and why

Four worked examples load with one click, one demonstrating each verdict, all drawn from clinical data and digital health: ML-assisted CDISC mapping (Scale), GenAI drafting of data management plans (Proceed), autonomous EDC query resolution (Pivot), and autonomous eligibility screening in a decentralized trial (Stop). You can see how the same engine separates a low-risk internal tool from a high-stakes autonomous one.

## Design decisions

I made four choices on purpose, because a tool that scores AI risk should hold itself to the same standard it applies.

**It is deterministic. No model judges your use case.** The scoring is a fixed rule set, so the same inputs always give the same verdict, and every point traces back to an answer you selected. A black-box tool for assessing black-box risk would defeat the purpose.

**The weights are visible and editable.** Defaults reflect a regulated posture, with risk and responsible-design weighted higher. You can change them, so the tool imposes no hidden value judgment.

**Guardrails can only lower a verdict, never raise it.** A data-protection red line, an evaluation gate, an autonomy-versus-stakes check, and a critical-risk ceiling can each cap the result regardless of how strong the rest of the score looks. The panel shows which one fired.

**It runs entirely in your browser.** Nothing you type leaves the page. No storage, no analytics, no network calls. Privacy by design, not as an optional setting.

## How scoring works

Each dimension is scored from its questions on a 0 to 100 scale. The composite is a weighted average of feasibility, evaluation, an inverted risk score (lower risk scores higher), and responsible-by-design. The composite maps to a base verdict by band: 75 and above is a Scale candidate, 55 to 74 is Proceed, 40 to 54 is Pivot, below 40 is Stop. Guardrails then apply and can only cap the result lower. The verdict you see is the lower of the base band and any guardrail ceiling.

## What the rubric considers

The live tool is a rapid triage: it surfaces the factors that move a verdict the most and applies neutral defaults to the rest, so you get an answer fast. The full rubric behind the engine weighs:

- **Feasibility:** problem definition and success metric, data availability and access, in technical approach.
- **Evaluation:** whether an evaluation method exists, and whether there is a ground-truth or expert benchmark to measure against.
- **Risk and failure modes:** hallucination and factual error, data leakage, workflow fit and adoption, scalability, vendor overclaim and lock-in, and the consequence if the system is wrong.
- **Responsible-by-design:** data privacy and handling, auditability and traceability, GxP and regulatory validation fit, human oversight matched to the stakes, and bias checks along with subgroup fairness.

## Methodology and assumptions

The rubric is informed by recognized responsible-AI frameworks, adapted for clinical and digital-health work: the NIST AI Risk Management Framework, the OECD AI Principles, the EU AI Act's risk-tiering logic, Good Machine Learning Practice for medical-device software, and WHO guidance on AI for health.

A few assumptions are stated rather than hidden:

- The composite is compensatory (a strength can offset a weakness), but the guardrails are not. They enforce non-negotiable floors and can only lower a verdict.
- Every guardrail keys off a high-signal question the user actually answers, so the rapid triage cannot hide a red line behind a default.
- The band thresholds and dimension weights are reasoned conventions calibrated for a regulated posture, not empirically validated cutoffs, and the weights are visible and adjustable.
- It is a self-assessment, so a second independent reviewer reduces individual bias.

## How I built it

I designed the rubric. The dimensions, the questions, the severity levels, the gating logic, and the weighting come from my experience in clinical data management and digital health inside highly-regulated environments. This judgment in design choices is the part that matters.

I used Claude to generate the implementation. I specified the model, reviewed the logic, and wrote a small test that runs all four examples through the scoring engine to confirm each produces the intended verdict before shipping. The code is AI-assisted. The criteria, the decisions, and the verification are my own.

I am stating this plainly because building responsibly with AI includes being honest about how you built it.

## Limitations

This is a decision-support aid, not a decision-maker. The verdict reflects what you enter, which is an estimate. It does not replace a Data Protection Impact Assessment, GxP validation, a security review, or sign-off from accountable owners. The weights and thresholds are considered judgment calls, not validated against an external benchmark. Treat the output as a structured starting point for a conversation, not a control.

## Tech

One self-contained HTML file. Basic JavaScript, no framework, no build step. The only external dependency is Google Fonts. Deploys as-is to GitHub Pages, Netlify, Vercel, Cloudflare Pages, or any static host.

To run locally, open `index.html` in a browser. To deploy, drop the file on any static host and point people at the URL.

## About

I am Caroline Flessa, MPH, a clinical data and digital health professional. I work on clinical data governance, EDC and eCOA implementations, CDISC standards in clinical data review, and have become much more interested in responsible uses of AI in regulated research settings. Please reach out with any questions or comments.

---

*Built with AI assistance and human judgment. The scoring methodology is my own; the implementation was generated with Claude and verified by me.*

## License
© 2026 Caroline Flessa. All rights reserved. See LICENSE. Made available for demonstration and evaluation only.
