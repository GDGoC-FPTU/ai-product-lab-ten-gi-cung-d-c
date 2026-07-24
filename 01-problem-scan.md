# 01 - Problem Scan

**Student:** ........................................

**Student ID:** ....................................

---

# Phase 1 — SCAN

| # | Subsidiary | Lens | Problem |
|---|------------|------|---------|
| 1 | Xanh SM | Time-consuming | Dispatchers manually handle low-battery incidents by checking vehicle location, battery percentage, charging station availability, and composing instructions for drivers. |
| 2 | Xanh SM | Stakeholder Pain | Drivers complain that suggested pickup/drop-off points are inaccurate for apartment entrances, taxi lanes, or restricted stopping areas. |
| 3 | VinFast | AI-upgrade | Customer service agents manually read customers' descriptions of vehicle issues before routing them to technical teams. |
| 4 | Vinhomes | Repetitive | Property management staff manually classify and route resident complaints (elevator, water, noise, parking, etc.). |
| 5 | Vinmec | Time-consuming | Doctors spend significant time preparing discharge summaries from medical records and test results. |
| 6 | Vinpearl | Stakeholder Pain | Managers manually review hotel feedback across multiple platforms to identify urgent complaints.

---

# Phase 2 — Quick Problem Cards

## Quick Problem Card #1 — Xanh SM Battery Incident Dispatcher

### Problem
Drivers report low battery while on duty and dispatchers must quickly identify an appropriate charging station or arrange mobile charging.

**Company**

- ☑ Xanh SM

### Actor

- Driver
- Dispatcher
- Passenger

### Current Workflow

1. Driver reports low battery
2. Dispatcher checks GPS and battery level
3. Dispatcher searches VinFast charging stations
4. Dispatcher drafts guidance
5. Dispatcher dispatches rescue/mobile charger if necessary

### Bottleneck

Searching charging stations and composing guidance.

**Average Time:** 10–12 minutes

### AI Opportunity

AI summarizes available charging options and drafts dispatcher guidance.

### Success Metric

- Reduce handling time from **15 minutes** to **under 3 minutes**
- **100%** of responses reviewed by dispatcher before sending

### Architecture

**LLM Feature**

---

## Quick Problem Card #2 — Vinhomes Complaint Classification

### Problem

Automatically classify resident complaints and route them to the correct department.

### Actor

- Property manager
- Technical staff
- Residents

### Workflow

1. Resident submits complaint
2. Staff reads complaint
3. Categorize issue
4. Route ticket
5. Monitor SLA

### Bottleneck

Manual reading and routing.

**Average Time:** 8–10 minutes

### AI Opportunity

Intent classification, urgency detection, and first-response drafting.

### Success Metric

- 85% routing accuracy
- First response reduced from **2 hours** to **15 minutes**

### Architecture

**LLM Feature**

---

## Quick Problem Card #3 — VinFast Vehicle Fault Classification

### Problem

Customers describe vehicle issues in natural language.

### Actor

- Customer Service
- Technician
- Customer

### Workflow

1. Customer submits issue
2. Agent asks follow-up questions
3. Agent classifies issue
4. Transfer to technician
5. Schedule service

### Bottleneck

Manual interpretation of issue descriptions.

**Average Time:** 12 minutes

### AI Opportunity

Summarize symptoms, suggest issue category, recommend follow-up questions.

### Success Metric

- Reduce classification time to under **3 minutes**
- 90% complete information before technician assignment

### Architecture

**LLM Feature**

---

# Selected Problem

The team selected **Quick Problem Card #1 — Xanh SM Battery Incident Dispatcher** for the Deep Dive phase.

Reasons:

- Clear workflow
- Measurable bottleneck
- Human approval can remain mandatory
- Easy to prototype using Gemini