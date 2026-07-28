# Compliance

Anti-spam and privacy law applies to every marketing email. This is a practical guide, not legal advice — for edge cases, tell the user to consult a lawyer. The safe strategy is simple: **meet the strictest applicable standard and every other regime is satisfied.**

## The Universal Minimum (every marketing email, everywhere)

- **Working unsubscribe link** that takes effect promptly (CAN-SPAM allows 10 business days; MailerLite applies it immediately — never circumvent this).
- **Honest subject line and sender identity** — no deceptive "Re:"/"Fwd:", no misleading from names.
- **Physical mailing address** of the sender in the footer (P.O. box is fine).
- **Provable consent** for every recipient (when/where/how they opted in).
- Never email people who unsubscribed, hard-bounced, or complained. MailerLite enforces these statuses — do not work around them by re-importing addresses.

## GDPR (EU/EEA recipients — and UK GDPR)

- Consent must be **freely given, specific, informed, and unambiguous**: unticked checkboxes, no consent bundled into unrelated terms, clear statement of what they're signing up for.
- Keep **records of consent** — MailerLite stores signup source, timestamp, and IP for form signups; this is the audit trail, another reason to grow lists through forms rather than imports.
- Subscribers have the right to **access and erasure**: on request, export a subscriber's data or delete ("forget") them fully — deletion, not just unsubscribing.
- **Double opt-in is effectively mandatory in Germany and Austria** (case law) and best practice for all EU audiences.
- A soft exception exists for **existing customers** being marketed similar products/services (opt-out basis), but it's narrow — when in doubt, get opt-in consent.

## CAN-SPAM (US recipients)

- Opt-out based rather than opt-in: mailing without prior consent isn't automatically illegal, but every message needs identification, address, and unsubscribe — and non-consented cold email destroys deliverability regardless of legality, so recommend against it anyway.
- Unsubscribe requests must be honored within 10 business days and the unsubscribe mechanism must work for 30+ days after sending.
- No fees, logins, or extra steps to unsubscribe.

## CASL (Canadian recipients) — the strict one

- Requires **express or implied consent before sending**. Implied consent (existing business relationship) expires — generally 2 years after the transaction.
- Consent records are mandatory; penalties are severe (up to CAD 10M).
- Treat Canadian recipients as opt-in only, with documented consent.

## Practical Rules for Agents

1. **Growing lists**: always through forms (embedded, popup, landing page) with clear language about what subscribers will receive. Recommend double opt-in by default.
2. **Imports**: ask about consent provenance before importing ("When and how did these people sign up?"). Refuse purchased/scraped lists outright.
3. **Lead magnets**: delivering the freebie is fine; adding them to ongoing marketing requires that the form said so.
4. **Checkbox pre-ticking, hidden opt-ins, consent buried in T&Cs**: refuse — invalid under GDPR and CASL.
5. **Re-adding unsubscribed users**: refuse unless the person demonstrably re-subscribed themselves (new form signup). "They unsubscribed by accident" requires them to opt back in, not an import.
6. **Deletion requests**: use full subscriber deletion (not unsubscribe) for GDPR erasure requests, and confirm before executing — it's irreversible.
7. **Sensitive data** (health, finances, minors): extra caution; suggest legal review before campaigns targeting these categories.
8. **B2B is not exempt**: GDPR and CASL apply to business email addresses too.

## Transactional vs Marketing

Order confirmations, receipts, and password resets are transactional and exempt from most marketing rules — but only while they stay transactional. Adding promotional content to a receipt can reclassify it. Keep transactional sends (via a transactional email service such as MailerSend, or SMTP) separate from marketing campaigns, and never use transactional channels to reach unsubscribed marketing contacts.
