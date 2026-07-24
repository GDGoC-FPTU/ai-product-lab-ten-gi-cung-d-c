# 02 - Deep Dive Report

# Team Information

**Team Name:** ___________________________

| Name | Student ID |
|------|------------|
| | |
| | |
| | |

---

# Selected Problem

**Xanh SM AI Co-pilot for Low Battery Incident Handling**

---

# 3.1 Current-State Workflow

```text
Driver reports low battery
        │
        ▼
Dispatcher receives call (2 min)
        │
        ▼
Lookup GPS & Battery (2 min)
        │
        ▼
Lookup charging station (5 min)
        │
        ▼
Compose instructions (5 min)
        │
        ▼
If battery <5%
Dispatch mobile charger
```

Total processing time

**≈15 minutes per incident**

Main bottleneck

- Charging station lookup
- Manual instruction writing

---

# 3.2 Problem Statement

| Field | Description |
|-------|-------------|
| Actor | Xanh SM Dispatcher |
| Current Workflow | Dispatcher manually checks GPS, battery level, charging stations, then writes instructions for drivers. |
| Bottleneck | Charging station lookup and instruction drafting take approximately 10 minutes. |
| Business Impact | Around 20 dispatcher-hours lost daily if handling roughly 80 incidents/day. Delays increase customer waiting time and cancellations. |
| Success Metric | Average handling time <3 minutes; 95% complete drafts; 100% dispatcher approval before sending. |
| Operational Boundary | AI drafts recommendations only. AI cannot send messages automatically or invent charging station information. Human approval is mandatory. |

---

# 3.3 Future-State Workflow

```text
Driver reports issue
        │
        ▼
System retrieves GPS, battery, vehicle information
        │
        ▼
Rule Engine checks safety boundary
        │
        ▼
LLM drafts recommendation
        │
        ▼
Dispatcher reviews
        │
        ▼
Dispatcher approves
        │
        ▼
Driver receives guidance
```

---

# AI Fit

✅ LLM Feature

Rule-based logic remains responsible for:

- Battery threshold
- Distance threshold
- Safety rules

LLM is responsible for:

- Summarization
- Draft generation
- Natural language response

---

# Human-in-the-Loop

Dispatcher must approve every AI-generated recommendation before it is delivered.

---

# Fallback

If AI:

- produces invalid output
- lacks confidence
- fails JSON validation
- experiences prompt injection

the dispatcher immediately returns to the existing manual workflow.

---

# Phase 5 — Evaluation

## AI Readiness Checklist

| Question | Status |
|----------|--------|
| Clean historical logs available | Partial |
| AI errors controllable | Yes |
| Stakeholders willing to adopt | Yes |

---

# Final Decision

✅ **GO**

Prototype should begin with a limited internal deployment.

---

# Justification

The workflow is clearly defined, measurable, and repetitive.

The bottleneck is concentrated in language-heavy tasks where LLMs perform well.

Safety risks remain manageable because:

- AI never makes the final decision.
- Dispatcher approval is mandatory.
- Hard safety rules remain rule-based.

Estimated prototype timeline:

- Week 1: Data collection
- Week 2: LLM API integration
- Week 3: Dispatcher review interface

The project should remain internal until production performance has been validated.