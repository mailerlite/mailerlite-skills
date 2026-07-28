# Campaign Checklist

Detailed guidance for planning, writing, testing, and evaluating one-time campaigns.

## Pre-Send Checklist

Run through this before any send or schedule action:

- [ ] **Goal**: one campaign, one goal, one primary CTA
- [ ] **Audience**: correct group/segment selected; subscriber count checked and stated to the user
- [ ] **Sender**: verified `from` address on a custom domain; recognizable `from_name` (brand or person@brand); `reply_to` goes to a monitored inbox — never a no-reply address
- [ ] **Subject**: under ~60 characters, specific, honest, no spam patterns
- [ ] **Preheader**: set deliberately; complements the subject (default is the email's first line, often "View in browser" — avoid that)
- [ ] **Content**: mobile-rendered check, one clear CTA above the fold, working links, alt text on images, text-to-image balance (never image-only)
- [ ] **Personalization**: every merge field has a fallback (`{$name|default:('there')}`); no broken `Hi ,`
- [ ] **Footer**: unsubscribe link + physical mailing address present (MailerLite templates include these — do not remove)
- [ ] **Test**: test email sent or dashboard preview reviewed
- [ ] **Timing**: scheduled (not instant) unless the user explicitly wants instant; user confirmed the send

## Subject Lines

What works:

- **Specific beats clever**: "3 pricing mistakes freelancers make" > "You won't believe this"
- **Front-load the value** — mobile clients truncate around 30–40 characters
- **Personalization helps modestly** — name or topic relevance; don't force it
- **Numbers and concrete outcomes** perform reliably
- **Questions** work when the email actually answers them

What hurts:

- ALL CAPS, multiple exclamation marks, "FREE", "$$$", "act now", "limited time!!!" — spam-filter and human-filter triggers
- Deceptive subjects ("Re:", "Fwd:" on a first touch) — illegal under CAN-SPAM and destroys trust
- Emoji walls — one emoji can work for some brands; three is noise
- Clickbait that the body doesn't pay off — inflates opens once, kills them long-term

Always propose 2–3 options. For lists of roughly 1,000+ recipients, propose an A/B (`ab` type) campaign instead of guessing.

## A/B Testing

- Test **one variable at a time**: subject line, from name, send time, or content — not several at once.
- Subject line tests are the highest-leverage and cheapest to run.
- Sample size matters: below ~1,000 recipients, differences are usually noise; just pick the better-practice option.
- Let MailerLite pick the winner by opens (subject/from tests) or clicks (content tests); clicks are the more trustworthy metric post-Apple-MPP.
- Keep a running note of what won — subject style learnings compound across campaigns.

## Send Timing

- There is no universal best time. Mid-week mid-morning is a fine default for B2B; evenings and weekends often work for consumer/creator lists.
- Prefer MailerLite's `timezone_based` delivery for geographically spread lists, and `smart_sending` (per-subscriber optimized time) when engagement history exists.
- Consistency beats optimization: a newsletter that arrives every Tuesday builds a habit.
- Avoid stacking sends: leave breathing room between campaigns to the same audience (as a default, no more than one marketing send per audience per day, and watch unsubscribe rates as frequency rises).

## Auto-Resend

MailerLite's `resend` campaign type re-sends to non-openers with a different subject line:

- Wait at least 24–48 hours after the original send.
- Change the subject line — same subject to the same non-openers is pointless.
- Use sparingly (major announcements, deadlines), not on every newsletter — non-openers who get every email twice unsubscribe or complain.

## Post-Send Analysis

Pull campaign stats about 24–48 hours after sending. Evaluate against these thresholds:

| Metric | Healthy | Investigate | Stop and fix |
|---|---|---|---|
| Open rate | > 30% | 15–30% | < 15% |
| Click rate (of delivered) | > 2% | 1–2% | < 1% |
| Click-to-open rate | > 10% | 5–10% | < 5% |
| Unsubscribe rate | < 0.2% | 0.2–0.5% | > 0.5% |
| Hard bounce rate | < 0.5% | 0.5–2% | > 2% |
| Spam complaint rate | < 0.02% | 0.02–0.1% | > 0.1% |

Interpretation notes:

- **Apple Mail Privacy Protection auto-fires opens** for a large share of Apple Mail users, inflating open rates. Treat opens as directional; treat **clicks as the real engagement signal**.
- Good opens + poor clicks → subject over-promised or content/CTA under-delivered.
- Rising unsubscribes → frequency or relevance problem; check what changed.
- Any spike in bounces or complaints → deliverability issue; consult `deliverability.md` before the next send.
- Use link-level click reports to learn which topics/CTAs the audience actually wants.
