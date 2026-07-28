# Automation Playbooks

Standard automation flows with triggers, timing, and content guidance. Adapt counts and delays to the user's business; these are proven defaults, not laws.

General rules for all automations:

- Build the flow, walk the user through it (trigger → steps → conditions), then activate — never activate silently.
- Every email in a flow needs an unsubscribe link and honest subject.
- Delays are measured in hours and days, not minutes. Rapid-fire sequences read as spam.
- One idea per email. If an email has three topics, it's three emails (or two too many).
- Check the trigger can't double-fire (e.g. re-joining a group) unless repeat entry is intended.

## Welcome Series

The highest-ROI automation. New subscribers are at peak attention — welcome emails earn several times the engagement of regular campaigns.

**Trigger:** subscriber joins the main group (via form or import consent flow).

| Step | Timing | Content |
|---|---|---|
| Email 1 | Immediately | Deliver what was promised at signup (lead magnet, discount, confirmation of what to expect). Set expectations: what they'll receive and how often. Single CTA. |
| Email 2 | +2 days | Your best content or story — why this list is worth staying on. Introduce the brand/person behind it. |
| Email 3 | +3–4 days | Social proof, most popular resource, or best-seller. Soft CTA toward the core product/action. |
| Email 4 (optional) | +4–5 days | Segmentation ask ("what are you most interested in?" — clicks add to interest groups) or direct offer. |

Tips:
- Email 1 is often the highest-open email the account will ever send — don't waste it on "thanks for subscribing" alone.
- Exclude welcome-series recipients from regular campaigns during the series if send volume would stack up.

## Abandoned Cart (e-commerce)

**Trigger:** e-commerce integration cart-abandoned event.

| Step | Timing | Content |
|---|---|---|
| Email 1 | +1–4 hours | Simple reminder with cart contents and a direct "complete your order" link. No discount yet. |
| Email 2 | +24 hours | Address objections: shipping, returns, guarantees, reviews of the cart items. |
| Email 3 | +48–72 hours | Optional incentive (discount or free shipping) if margins allow. Warning: training customers to abandon carts for discounts is a real cost — recommend incentives only on the last email, or only for first-time buyers. |

## Post-Purchase

**Trigger:** e-commerce order-completed event.

| Step | Timing | Content |
|---|---|---|
| Email 1 | Immediately–1 day | Thank you + what happens next (shipping expectations, how to use the product). Transactional in tone. |
| Email 2 | +5–10 days (after delivery) | Usage tips, getting the most from the purchase. Builds review-readiness. |
| Email 3 | +2–3 weeks | Review request and/or cross-sell of a genuinely related product. |

Repeat buyers come from post-purchase experience, not from more promotions — keep this flow helpful, not salesy.

## Re-engagement (Win-back)

**Trigger:** subscriber joins an "inactive" segment (no opens/clicks in 90+ days — see `segmentation.md`) using the "joins segment" automation trigger.

| Step | Timing | Content |
|---|---|---|
| Email 1 | Day 0 | "We miss you" / "Still want these emails?" — restate the value, best recent content, one-click way to stay. |
| Email 2 | +7 days | Different angle: preference update (reduce frequency, change topics) or an incentive if commercial. |
| Email 3 | +7 days | Honest goodbye: "we'll stop emailing unless you click" with a clear stay-subscribed link. |

**Critical:** the flow must have an exit. Subscribers who don't respond get unsubscribed or moved to a suppressed group (the "sunset"). Continuing to mail confirmed-dead addresses is the fastest way to the spam folder — see `deliverability.md`. Frame the removal as a win for the user's sender reputation, because it is.

## Birthday / Anniversary

**Trigger:** anniversary of a date field (birthday field, signup date).

- Single email, sent on or just before the date.
- Include something real (discount, gift, free month) — an empty "happy birthday" from a brand is noise.
- Requires the date field to exist and be populated; check field coverage before proposing this flow. If only a small fraction of subscribers have the field, suggest collecting it via a preference form first.

## Lead Nurture / Course Sequence

**Trigger:** joins a topic group (downloaded a lead magnet, enrolled in a free course).

- 4–7 emails, each 2–3 days apart, moving from education → application → offer.
- Front-load value: the first 60–70% of the sequence should ask nothing.
- End with a clear offer email and, optionally, a deadline email 2 days later.
- Move completers into the main newsletter group; don't leave them in a dead-end.
