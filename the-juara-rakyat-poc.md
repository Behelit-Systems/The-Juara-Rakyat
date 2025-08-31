# Universal Prompt & Agent Design — *Juara Rakyat PoC*

> Drop this Markdown into any repo. Fill `[brackets]`. This is intentionally model- and platform-agnostic (works with Claude, GPT/Gemini families, or future LLMs) and enforces a strict contract so prompts are reproducible, testable, and safe.

---

# 0. File / Metadata

**Filename suggestion:** `juara-rakyat-poc-agent.md`
**Version:** v1.1 — PoC (WhatsApp-first OSINT + Scambaiting + Folder/Tech Reference)
**Purpose:** Single-source template for Juara Rakyat agents, prompt contracts, tool definitions, project structure, tech stack, and evaluation.
**How to use:** Duplicate per agent (osint\_agent, detection\_agent, scambaiter\_agent, hunting\_agent, modeling\_agent), fill `[brackets]`, adapt `TOOLS` and `OUTPUT` schemas.

---

# 1. Quick Rules (Always follow)

1. Use **PT-CF** header for every agent prompt: **Persona — Task — Context — Format**.
2. Declare measurable success criteria before running agent.
3. Return only validated outputs (JSON or defined Markdown schema).
4. Log every tool call, prompt input, and model metadata.
5. Return “I don’t know” if uncertain; include verification steps.
6. Escalate or refuse any output violating law, policy, or PII safeguards.

---

# 2. PT-CF Prompt Contract (copy this block exactly)

```
PERSONA:
You are a Juara Rakyat agent ([osint|detection|scambaiter|hunting|modeling]). Tone: professional, precise.

TASK:
Primary task: Process input messages/artifacts, detect scams, enrich intelligence, or perform sandboxed scambaiting.
Success criteria: All MCP envelopes processed, alerts enriched, scambaiting logged in sandbox mode. No external live messages unless operator approves.
Non-goals: Do NOT perform real-world phishing, spamming, or unauthorized network access.

CONTEXT:
- Facts: WhatsApp-first PoC, MCP-style canonical envelopes, NATS JetStream messaging.
- Attachments: ingest.raw.*, ingest.mcp.*, enrichment responses.
- Constraints: Sandbox-only by default; SCAMBAITING_SANDBOX=true.

FORMAT:
Return ONLY the following format: JSON matching MCP-style schema / alert schema / session schema.
Validate against schema before output.

TOOLS:
- `vt_check` → Input: MCP envelope → Output: enrichment scores
- `phishtank_lookup` → Input: URL list → Output: phishing verdicts
- `osint_enrich` → Input: entity list → Output: enriched info
- `audit_log` → Input: action/event → Output: confirmation hash

RULES:
- Safety: never output PII or live scam interactions unless explicitly approved.
- Escalation: handoff if validation fails, operator approval missing, or external live action requested.
- Stop condition: session complete, or max steps reached.
```

---

# 3. Reusable System Block

```
SYSTEM:
Enforce PT-CF. Validate MCP envelopes, detection alerts, enrichment outputs. Retry 2 times on validation failure; escalate afterward.

LOGGING:
Emit structured log per run:
{
  "prompt_id": "...",
  "agent": "[agent_name]",
  "model": "...",
  "version": "...",
  "tools_used": [...],
  "timestamp": "ISO8601"
}

CONFIDENTIALITY:
Redact phone numbers, emails, or PII. Store audit logs only in MinIO with immutable hash.
```

---

# 4. Tools

* `vt_check` → Input: `{ "urls": [], "hashes": [] }` → Output: `{ "scores": [{ "url": "...", "malicious": true|false }] }`
* `phishtank_lookup` → Input: `{ "urls": [] }` → Output: `{ "results": [{"url":"...","phish":true|false}] }`
* `osint_enrich` → Input: `{ "entities": [] }` → Output: `{ "enriched": [{ "entity":"", "info":{} }] }`
* `audit_log` → Input: `{ "action": "string", "payload": {} }` → Output `{ "status":"ok|error", "hash":"..." }`
* `human_approve` → Input: `{ "ticket": {...} }` → Output `{ "approved": true|false, "reviewer": "..." }`

---

# 5. Minimal Agent Loop

```
state = {goal, context, history: []}
for step in 1..MAX_STEPS:
  plan = LLM(plan_prompt(state))
  if plan.intent == "finish":
    output = LLM(format_prompt(state))
    if validate(output): return output
    else: append validation errors; retry 2x
  elif plan.action:
    tool_input = sanitize(plan.action.input)
    tool_output = call_tool(plan.action.name, tool_input)
    append tool_output to state.context
  if violates_guardrails(state): escalate_to_human()
end
return {"status":"needs_human","reason":"max_steps_exceeded"}
```

---

# 6. Output Schemas

**MCP envelope**

```json
{
  "mcp_version": "1.0",
  "event_id": "uuid-v4",
  "timestamp": "ISO8601",
  "origin": { "connector": "whatsapp", "group_id": "", "source_id": "" },
  "payload": { "text": "", "attachments": [], "meta": {} },
  "entities": [{ "type":"phone","id":"", "confidence":0.0 }],
  "trace": { "ingest_trace": [] },
  "signatures": []
}
```

**Detection alert**

```json
{
  "alert_id": "uuid-v4",
  "mcp_event": "uuid-v4",
  "type": "scam|phish|malware",
  "confidence": 0.0,
  "recommendation": "sandbox|escalate|ignore",
  "timestamp": "ISO8601"
}
```

**Scambaiter session**

```json
{
  "session_id": "uuid-v4",
  "alert_id": "uuid-v4",
  "sandboxed": true,
  "messages": [],
  "audit_hash": "sha256"
}
```

---

# 7. Guardrails & Safety

* **PII redaction:** phone, email, national ID.
* **Sandbox default:** SCAMBAITING\_SANDBOX=true.
* **Refusal:** no phishing, malware, or law-breaking outputs.
* **Audit:** all actions logged with immutable hash in MinIO.
* **Legal compliance:** operator must approve live actions; jurisdictional document required.

---

# 8. Project Main Objectives

1. Deploy a **sandboxed WhatsApp-first OSINT + scambaiting PoC**.
2. Process messages through MCP canonical envelopes.
3. Detect scam, phishing, and malware events.
4. Enrich intelligence via OSINT connectors.
5. Provide scambaiting sessions **sandboxed** for safe testing.
6. Ensure **auditability** and reproducibility for every agent action.

---

# 9. Project Tech Stack

* **Languages:** Python 3.12+ (core PoC), optional Go for NATS adapters
* **Messaging:** NATS JetStream (MCP envelope transport)
* **Database:** MinIO (immutable audit), optional PostgreSQL for enrichment cache
* **ML/Classifier:** CPU-friendly Python classifiers, optional PyTorch/BERT
* **APIs/Connectors:** WhatsApp Business API (sandbox for PoC), OSINT tools (VirusTotal, Phishtank)
* **Containerization:** Docker, Kubernetes-ready
* **Monitoring:** Structured JSON logs + optional Prometheus/Grafana

---

# 10. Project Folder Structure

```
juara_rakyat_poc/
├─ agents/
│  ├─ osint_agent.py
│  ├─ detection_agent.py
│  ├─ scambaiter_agent.py
│  ├─ modeling_agent.py
│  └─ hunting_agent.py
├─ connectors/
│  ├─ whatsapp_sandbox.py
│  ├─ vt_connector.py
│  └─ phishtank_connector.py
├─ ingest/
│  ├─ ingest_raw.py
│  └─ ingest_mcp.py
├─ schemas/
│  ├─ mcp_schema.json
│  ├─ alert_schema.json
│  └─ session_schema.json
├─ tests/
│  ├─ unit/
│  └─ integration/
├─ scripts/
│  ├─ bootstrap_dataset.py
│  └─ validate_schemas.py
├─ logs/
│  └─ audit/
├─ docker/
│  └─ Dockerfile
└─ README.md
```

---

# 11. Project Software Practices

* Modular agent design; agents communicate via canonical MCP envelopes
* **Validation-first:** always enforce schema validation before logging or alerting
* Sandbox vs live separation strictly enforced
* Immutable audit trails in MinIO, hash-verified
* CI/CD with automated tests for MCP, alerts, scambait sessions
* Optional ML/AI models abstracted to enable PyTorch/BERT integration later
* Golden dataset for evaluation; human review required for edge cases

---

# 12. Evaluation Pack

* Golden set: 10–20 dummy WhatsApp/Telegram messages (loan scam, MLM, crypto).
* Automated checks: MCP envelope validation, alert classification, enrichment output.
* Human rubric: Accuracy 0–5, Completeness 0–5, Safety 0–5.
* Release gate: ≥95% pass on automated and human checks.

---

# 13. Deployment Checklist

* [x] Folder structure and agents scaffolded
* [x] NATS subjects and MCP schema defined
* [x] Ingestion adapters implemented (sandbox/mock)
* [x] Detection + OSINT + Scambaiter skeletons
* [x] Dataset bootstrap script added
* [x] Dummy test framework in place
* [x] Operator docs and scambaiting legal flow created
* [ ] Optional: connect production WhatsApp Business API
* [ ] Optional: integrate full ML models (PyTorch/BERT)

---

# 14. Juara Rakyat PoC Notes

* PoC is **WhatsApp-first** with sandbox-only scambaiting.
* PyTorch or heavy ML is **not required**; small CPU-friendly classifiers used.
* Fully modular for later addition of domain agents, ML models, and live operations.
* All agents communicate via **NATS JetStream**, using canonical MCP envelopes.

---



---

# 📜 License

**License:** GNU Affero General Public License v3.0 (AGPLv3)

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published by
the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program. If not, see <https://www.gnu.org/licenses/>.

**SPDX-License-Identifier:** `AGPL-3.0-or-later`

A full `LICENSE` file with the complete AGPLv3 text must also be included at the repo root.


