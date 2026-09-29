# Capstone Final Ethics, Fairness & Privacy Policy (ETHICS.md)

**Emganwini Nedbank Hub | Master Project Portfolio**  
*Capstone Compliance Deliverable*

---

## 🛡️ 1. AI Feature Description
NedPulse operates as an automated financial copilot assisting clients with credit education, rate calculations, notice deposit guidelines, and financial disclosure summarization. It is strictly designated as an educational and advisory copilot, not an autonomous credit adjudicator.

---

## ⚖️ 2. Potential Biases Identified
1. **Linguistic & Jargon Bias**: Standard LLMs often assume high baseline financial literacy or English idiom familiarity, disadvantaging multilingual South African communities.
2. **Income & Credit Profile Skew**: Prompts may implicitly favor high-net-worth investment profiles over low-to-middle income financial instruments (e.g. entry-level transactional accounts or FLISP subsidies).
3. **Geographic & Demographic Disparity**: Default training data could recommend urban-centric banking infrastructure, overlooking informal or rural transaction workflows.

---

## 🛠️ 3. Mitigation Strategies
- **Plain Language Calibration**: System prompts instruct responses to be written in straightforward, accessible English without unnecessary jargon.
- **RAG Knowledge Grounding**: Answers regarding credit criteria are restricted to official Nedbank documents and the South African National Credit Act (NCA).
- **Proactive Inclusivity**: Explicit knowledge base inclusions for entry-level products (e.g., MiGoals, FLISP subsidies, youth accounts).

---

## 🔍 4. Transparency & Explainability
- Every conversational interaction displays a clear disclaimer: *"NedPulse is an AI copilot providing financial information. Consult an accredited Nedbank financial advisor for binding investment contracts."*
- RAG queries disclose source citations, providing chunk IDs and excerpts directly to the user.

---

## 🔒 5. Data Privacy & POPIA Compliance
- **Zero Training on Customer Data**: Prompt payloads submitted to third-party models are never retained for model retraining.
- **Personally Identifiable Information (PII) Redaction**: Financial account numbers and ID numbers are masked before external API dispatch.
- **Right to Erasure**: Users have the ability to clear or permanently archive their conversation history at any time.
