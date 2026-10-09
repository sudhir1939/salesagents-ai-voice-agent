# AI Voice Qualification Agent - Home Credit LAP

Automated AI Voice Agent developed for **Home Credit** to qualify existing customers for a pre-approved Loan Against Property (LAP) offer up to ₹75,00,000.

## 🔗 Live Agent & Artifacts
- **Published Agent Link:** [Retell AI Agent](https://agent.retellai.com/orb/agent_8affcf1e14166ae34dfefb453b?token=9e30cc3b4457d3a72e05d493401f0f61)
- **Screen Recording Demo:** [Google Drive Video Link](https://drive.google.com/drive/folders/11UFyOmiCiabyVLBIuQE1pgtPbKNOLPPP?usp=sharing)
- **Full Prompt File:** [`system_prompt.md`](./system_prompt.md)

---

## 🏗️ Architecture & Conversational State Machine
The agent implements an **Extract -> Validate -> Update State -> Ask First Missing Question** pipeline:

1. **State Tracking:** Tracks 7 variables (`property_type`, `ownership_status`, `documents_available`, `loan_amount`, `occupation_and_income_mode`, `market_value`, `tenure`).
2. **Out-of-Order Entity Extraction:** Captures multi-entity customer utterances (e.g., "It's a residential flat worth 1 Cr, solely owned") in a single turn without re-asking captured points.
3. **Immediate Disqualification Gate:** Instantly terminates with a polite exit if agricultural property, cash income, photocopy-only documents, or out-of-range tenures are stated.
4. **Loan Transfer Switch:** If existing property loans or EMI reduction requests are detected, switches off standard qualification and routes to a loan-transfer specialist.
5. **Loan Cap Negotiation:** Prompts a ₹75L ceiling counter-offer if the requested borrowing exceeds ₹75,00,000.
6. **Strict Handoff Enforcement:** Requires all 7 data points to be positively verified before triggering the senior loan expert handoff.

---

## 🧪 Verified Test Scenarios

| Test Case | Scenario / Utterance | Expected Behavior | Result |
| :--- | :--- | :--- | :--- |
| **Test 1** | Happy Path (Out-of-order details provided) | Extracts all details, asks missing items, hands off to expert | Passed |
| **Test 2** | Disqualification (Agricultural Property) | Polite exit notice and immediate call termination | Passed |
| **Test 3** | Existing Loan / EMI Reduction | Routes to loan transfer specialist and exits | Passed |
| **Test 4** | Loan Amount > ₹75 Lakhs | Informs of 75L cap, asks confirmation to proceed at 75L | Passed |
| **Test 5** | Busy Customer | Captures preferred callback time and exits | Passed |

---

## ⚙️ Platform Configuration
- **Platform:** Retell AI
- **Architecture:** Single-Prompt Voice Agent
- **LLM Engine:** GPT-4o / GPT-4.1
- **Voice Pipeline:** Low-latency conversational STT/TTS with Barge-in enabled
