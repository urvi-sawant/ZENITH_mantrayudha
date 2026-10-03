
# NovaMart AI Customer Support Agent - Mantra Yudha Submission

## Overview
An agentic AI customer support system built using Gemini Pro (`gemini-3.8-flash` / `gemini-2.5-flash`) designed to process customer support inquiries for NovaMart. The agent operates on a 4-move decision engine (ANSWER, ASK, ACT, ESCALATE) backed by local database verification.

## Key Features
- **Ground Truth Verification**: All customer claims are cross-checked against `orders.csv`, `customers.csv`, and `conversations.json` before taking action.
- **Refund Capping & Policy Engine**: Automatically enforces maximum refund limits (`min(requested, order_total)`) to prevent excessive approvals.
- **Prompt Injection Defense**: Implements an instruction hierarchy (L1-L3) that wraps user inputs and rejects unauthorized overrides.
- **Ambiguity & Disambiguation**: Detects missing order IDs or vague requests and triggers an `ASK` move instead of hallucinating.

## Architecture & Decision Loop
1. **Understand**: Parses user intent (handles multi-intent requests).
2. **Verify**: Invokes tools (`get_order`, `get_customer`, `check_refund_eligibility`).
3. **Decide & Act**: Executes verified tool calls (`create_refund`, `escalate_to_human`) or queries clarification.

## Setup & Execution

### 1. Install Dependencies
```bash
pip install -r requirements.txt
