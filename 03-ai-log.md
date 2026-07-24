# 03 - AI Log

## Student

Name: _______________________

Student ID: __________________

---

# Reflection

## How AI Helped

During this lab, I used ChatGPT as a brainstorming partner to identify AI opportunities across the Vingroup ecosystem.

AI helped me:

- Generate operational pain points.
- Compare multiple AI use cases.
- Refine problem statements.
- Identify measurable success metrics.
- Improve workflow descriptions.
- Design operational boundaries for AI systems.

The discussion helped transform a general idea into a practical AI product proposal.

---

## Where AI Was Wrong

Initially, AI suggested building a fully autonomous dispatcher capable of making routing decisions and directly messaging drivers.

After reviewing the proposal, I realized this approach introduced unacceptable operational and safety risks.

AI also generated numerical estimates such as incident volume and handling time without access to internal company data. These values should only be considered assumptions for the lab rather than real business metrics.

---

## How I Improved the Prompt

I refined the prompt by introducing explicit operational boundaries.

The updated prompt instructed the AI that:

- It acts only as a dispatcher co-pilot.
- Every response must be labeled as a draft.
- Human approval is always required before sending instructions.
- If battery level is below 5% and no nearby charging station exists, the AI must recommend dispatching a mobile charger.
- Missing information must trigger clarification questions instead of hallucinated answers.

These constraints significantly improved the consistency and safety of the generated responses.

---

# Lessons Learned

The biggest lesson from this lab is that AI should support human decision-making rather than replace it.

Large Language Models are highly effective at summarizing information and drafting responses, but operational safety still depends on clearly defined rules, human oversight, and well-designed fallback mechanisms.

Designing the operational boundary is just as important as designing the AI prompt itself.