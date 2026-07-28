# Segmentation and Personalization

## Groups vs Segments

The single most common MailerLite modeling mistake is using the wrong one.

**Groups** are static labels. A subscriber is in a group because something *put them there*: a form submission, an import, an automation step, a manual action, or an API call. Membership never changes on its own.

Use groups for:
- Signup source ("Blog popup", "Webinar March 2026", "Shopify customers")
- Declared interests ("Wants product updates", "Recipes")
- Automation triggers (joining a group is the cleanest trigger)
- Suppression ("Sunset – do not email")

**Segments** are saved dynamic filters. Membership recalculates automatically as subscribers match or stop matching the rules.

Use segments for:
- Engagement tiers (opened/clicked recently vs not)
- Field values (country, plan, signup date ranges)
- Behavior (clicked a specific campaign link, bought from a category)
- Combinations (in group X AND inactive 90 days)

Rules of thumb:
- "Tag everyone who..." → usually a group (a fixed point-in-time action).
- "Everyone who is/has..." → usually a segment (an ongoing condition).
- Segments can filter *by* group membership, so groups are the raw material and segments are the queries.
- Don't create a group where a segment works — static copies of dynamic conditions go stale immediately.

## Engagement Tiers (the first segments every account needs)

| Segment | Rule (typical) | Treatment |
|---|---|---|
| Engaged | Opened or clicked in last 60–90 days | Full sending frequency; safe for new-domain warm-up |
| Cooling | No opens/clicks 60–90 days, was active before | Reduced frequency; best-content-only sends |
| Inactive | No opens/clicks in 90–180 days | Re-engagement automation only — never regular campaigns |
| New | Signed up < 14 days ago | In welcome series; consider excluding from big campaigns |

Because Apple Mail Privacy Protection inflates opens, prefer click-based rules where volume allows, or combine ("no click in 120 days") for stricter tiers.

## Common Segment Recipes

- **VIP / best customers**: 2+ orders, or total spent above a threshold (e-commerce fields) — deserve early access and non-promotional love.
- **Recent buyers**: order in last 30 days — exclude from discount promotions (nothing angers a customer like a coupon the week after they paid full price).
- **Geographic**: country/city field — event invites, shipping offers, timezone-appropriate content.
- **Topic clicks**: clicked links in campaigns about topic X — feed interest groups via automation for future targeting.
- **Form-specific**: signed up via a specific form — measure lead-magnet quality by downstream engagement.

## Personalization

- Personalize with **data, not just name**. "Products for your last purchase" beats "Hi John" every time.
- Every merge tag needs a fallback: `{$name|default:('there')}`. Check field fill-rates before personalizing — if 40% of subscribers lack a name, the fallback is doing most of the work.
- Match content to segment instead of one email for all: the same campaign duplicated with a changed intro per segment routinely outperforms generic sends.
- Don't be creepy: referencing behavior is fine ("you left this in your cart"), implying surveillance is not ("we noticed you've been reading our pricing page at 2am").

## Custom Fields

- Create fields for data that drives sending decisions (plan, city, birthday, last purchase category) — not for data that never affects an email.
- Prefer a few well-maintained fields over dozens of empty ones.
- Collect progressively: signup forms should ask for the minimum (email, maybe name); gather the rest via preference pages, surveys, and click-based inference.
