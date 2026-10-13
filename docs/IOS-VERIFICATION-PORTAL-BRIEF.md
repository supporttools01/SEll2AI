# iOS Data Verification Portal — Product Brief

## Goal
Build a new, original task-based verification portal with a crisp professional interface inspired by the workflow shown in the user's BidataBox screenshots. This should be a separate product concept and must not modify existing repositories or services outside this explicit target repository.

## Pricing target
- Target price: 4 USDT per 10,000 checks.
- Show unit price and estimated total before task submission.
- Validate balance server-side before queuing tasks.
- Credit only successful/actual provider-billed checks according to the configured provider contract; avoid silently charging for retries or failed requests.
- USDT payment/recharge remains unconfigured until an explicitly chosen compliant payment mechanism is implemented; never display a fake payment confirmation.

## Screens
1. Overview: balance, spend today/month, support information, task summaries.
2. iOS tasks: status verification and dynamic-status verification entries, batch TXT upload, task name, clear price estimate, country/region only if required by the authorized provider.
3. Task history: task ID/name, file, creation time, total records, result breakdown, cost, status, download actions.
4. Results: Activated / Unregistered / Inconclusive categories only when returned by a real authorized provider; demo jobs must be visibly marked DEMO.
5. User account: issued username, password reset, usage and audit history.
6. Admin: create/disable users, reset credentials, adjust credits/limits, manage pricing/provider settings, inspect audit logs.

## Design direction
- Distinct professional visual design: deep ink/navy or warm graphite, restrained teal/amber accents, generous spacing, careful contrast.
- Use ordinary production typography such as Inter, Geist, or system sans; do not use decorative AI-looking typefaces.
- Add modest layered depth through subtle shadows, fine borders, and small perspective/hover effects. Avoid excessive glassmorphism and neon gradients.
- Dense task tables should remain legible and responsive. The left navigation can collapse to icons on smaller widths.
- Original brand and components; don't copy BidataBox's logo or exact layout.

## Technical requirements
- Admin-issued user IDs; no public self-registration unless separately enabled.
- Passwords stored only as secure hashes; reset flows, rate limiting, session rotation, server-side role authorization.
- Ledger-based balance/credits with immutable transaction entries.
- Server-side upload size/type/line count checks; TXT file contains one record per line; reject malformed input and duplicate rows by explicit policy.
- Task queue with idempotency and retries that cannot double-charge.
- Export results with access checks; logs must not contain secrets or entire sensitive input lists.
- Retention controls and explicit disclosure for user-submitted data.

## Critical verification boundary
Only implement checks against data and provider APIs the operator is authorized to use. Do not request Apple IDs, passwords, OTPs, session cookies, or access private Apple account data. Do not claim to detect whether arbitrary phone numbers or accounts are activated unless a legitimate provider contract/API explicitly supports that use. Before a real provider is configured, provide a clear demo mode for format validation and synthetic sample data, not fabricated live results.

## Delivery sequence
1. UI prototype with realistic synthetic task data and clear DEMO labels.
2. Auth, users, admin roles, ledger and secure file validation.
3. Provider adapter contract and task queue; leave provider integration disabled until verified and approved.
4. Automated tests for pricing, permissions, uploads, charging, exports and error handling.
5. Deployment configuration and operational checklist.
