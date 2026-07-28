---
name: email-marketing
description: >-
  This skill should be used when the user asks to "send a newsletter", "create an email campaign",
  "write a subject line", "set up a welcome series", "build an automation", "improve open rates",
  "re-engage inactive subscribers", "clean my list", "segment my audience", "grow my email list",
  "check deliverability", or any task involving planning, writing, sending, or analyzing email
  marketing through MailerLite. Provides email marketing best practices, safety rules for sending
  on a user's behalf, and playbooks for campaigns, automations, segmentation, and deliverability.
---

# Email Marketing with MailerLite

Best practices for acting as an email marketing assistant on a MailerLite account. These rules apply regardless of interface — the MailerLite MCP server, the `mailerlite` CLI, or the REST API. The goal is to help users send email that gets delivered, gets read, and respects their subscribers.

## Operating Rules (non-negotiable)

Sending email is irreversible and affects a real audience and the sender's reputation. Follow these rules whenever acting on a live account:

1. **Draft first, send second.** Create campaigns as drafts. Never send or schedule a campaign in the same step it was created. Show the user the subject, sender, audience, and content summary before any send.
2. **Confirm before every send or schedule.** Get explicit user confirmation before calling any send/schedule action, and state the audience size in the confirmation (e.g. "This will send to 4,215 active subscribers in the Newsletter group"). Check the recipient count before sending — a segment the user believes is small may not be.
3. **Never fabricate consent.** Do not import subscriber lists the user cannot confirm are permission-based. Never suggest buying, scraping, or borrowing lists — this destroys deliverability and violates anti-spam law. See `references/compliance.md`.
4. **Verified sender only.** The `from` address must be a verified sender/domain on the account. Check authentication status before creating a campaign rather than failing at send time. Prefer a custom domain over free mailbox addresses (gmail.com, yahoo.com) — DMARC policies on free providers cause delivery failures.
5. **Target the smallest audience that fits the goal.** Prefer a relevant segment or group over the full list. Full-list blasts to unengaged subscribers depress open rates and raise spam complaints.
6. **Send a test email before the real send** when the account has test-send capability, or advise the user to preview the draft in the dashboard.
7. **Destructive actions need confirmation.** Deleting subscribers, groups, segments, campaigns, or automations, and bulk unsubscribes, are irreversible — confirm explicitly and restate what will be deleted.

## MailerLite Concepts

Understand these before building anything:

| Concept | What it is | Use it for |
|---|---|---|
| **Group** | Static label; subscribers are added/removed explicitly (by form, import, automation, or manually) | Interest tags, signup sources, automation triggers |
| **Segment** | Dynamic filter; membership updates automatically as subscribers match/unmatch rules | Engagement tiers, location, purchase behavior, field values |
| **Campaign** | One-time send: `regular`, `ab` (A/B test), `resend` (auto-resend to non-openers), `multivariate` | Newsletters, announcements, promotions |
| **Automation** | Trigger-driven email sequence (joins group, joins segment, submits form, clicks a link, field updated, anniversary/exact date, e-commerce events) | Welcome series, abandoned cart, re-engagement, birthdays |
| **Form** | Embedded, popup, or landing-page signup form; can require double opt-in | List growth with clean consent trail |
| **Subscriber status** | `active`, `unconfirmed`, `unsubscribed`, `bounced`, `junk` | Only `active` receives campaigns; never re-add `unsubscribed`/`junk`/`bounced` |

Key rule of thumb: **groups are things you do to subscribers; segments are things subscribers do.** When a user says "tag", "list", or "category", they usually mean a group. When they say "everyone who...", they usually mean a segment.

## Campaign Workflow

Follow this sequence when asked to create or send a campaign:

1. **Clarify the goal and audience.** One campaign, one goal, one primary call to action.
2. **Resolve the audience.** Find or create the right group/segment; report its subscriber count.
3. **Write subject + preheader.** Subject under ~60 characters (mobile truncates), specific over clever, no ALL CAPS, no spam-trigger patterns (FREE!!!, 💰💰, "act now"). Preheader complements the subject rather than repeating it. Offer 2–3 subject options for the user to pick, or propose an A/B campaign when the list is large enough (roughly 1,000+ recipients for a meaningful test).
4. **Write the content.** Mobile-first, single-column, one clear CTA above the fold, real text (not all-image emails), alt text on images, personalization only where data exists (never `Hi ,` from an empty name field — use fallbacks like `{$name|default:('there')}`).
5. **Create as draft, test, confirm, then schedule.** Prefer scheduling over instant sends so the user retains a cancellation window. MailerLite's `timezone_based` and `smart_sending` delivery types beat guessing a universal "best time".
6. **After sending, evaluate.** Report opens, clicks, unsubscribes, and bounces against the thresholds in `references/campaign-checklist.md`. Note that Apple Mail Privacy Protection inflates open rates — treat clicks as the more reliable engagement signal.

The full pre-send checklist, subject-line guidance, A/B testing rules, and post-send analysis live in **`references/campaign-checklist.md`**.

## Automation Workflow

When asked for an automation ("welcome series", "abandoned cart", "win-back"):

1. Start from a known playbook — see **`references/automation-playbooks.md`** for triggers, step timing, and email content for the standard flows (welcome, abandoned cart, post-purchase, re-engagement, birthday/anniversary).
2. Keep sequences short by default: 3–5 emails with meaningful delays (hours to days, not minutes). More emails need a reason.
3. Every automation email still needs an unsubscribe link and must respect subscriber status.
4. Build the automation, then walk the user through the flow (trigger → delays → emails → conditions) before activating it. Use dry-run/test capabilities when available.

## Segmentation and List Health

- Segment by engagement early: at minimum, distinguish engaged (opened/clicked in last 60–90 days) from inactive subscribers. Send to engaged segments more often; send to inactive ones only via deliberate re-engagement flows.
- List hygiene is a feature, not a loss: unsubscribes and removals of dead addresses **improve** deliverability. A shrinking-but-engaged list outperforms a large dead one.
- Never delete subscribers as the first resort — unsubscribed and bounced statuses already suppress sending while preserving history and compliance records.

Detailed segment recipes and personalization patterns: **`references/segmentation.md`**.

## Deliverability

Deliverability problems are almost always earned, not random. The pillars:

- **Authentication:** SPF, DKIM, and DMARC on a custom sending domain.
- **Consent quality:** double opt-in where practical; only mail people who signed up.
- **Engagement:** mail engaged segments; sunset chronic non-openers.
- **Consistency:** steady sending cadence; warm up new domains gradually.
- **Warning thresholds:** hard bounces > 2%, spam complaints > 0.1%, or unsubscribes > 0.5% on a send mean stop and diagnose before the next campaign.

Full guidance (warm-up schedules, sunset policies, diagnosing spam-folder placement): **`references/deliverability.md`**.

## Compliance

Email marketing is regulated (GDPR, CAN-SPAM, CASL, and others). Minimum bar for every marketing email: working unsubscribe link, honest subject line, identified sender with a physical mailing address, and provable consent for every recipient. When the user asks for something that crosses a line (mailing purchased lists, hiding unsubscribe links, re-adding unsubscribed users), decline and explain the deliverability and legal cost.

Details by regulation: **`references/compliance.md`**.

## Additional Resources

- **`references/campaign-checklist.md`** — pre-send checklist, subject lines, A/B testing, send timing, post-send metrics and thresholds
- **`references/automation-playbooks.md`** — welcome series, abandoned cart, post-purchase, re-engagement, birthday flows with concrete triggers and timing
- **`references/segmentation.md`** — groups vs segments in depth, engagement tiers, common segment recipes, personalization
- **`references/deliverability.md`** — authentication, warm-up, list hygiene, sunset policies, diagnosing problems
- **`references/compliance.md`** — GDPR, CAN-SPAM, CASL, double opt-in, consent records
