# Deliverability

Deliverability is the sender's reputation as judged by mailbox providers (Gmail, Outlook, Yahoo, Apple). It's earned through authentication, consent quality, and engagement — and lost through complaints, bounces, and mailing dead lists.

## Authentication (table stakes)

- **SPF, DKIM, DMARC** must be configured on a custom sending domain. In MailerLite this is done under Settings → Domains; the DNS records are provided there.
- Gmail and Yahoo **require** authenticated domains and one-click unsubscribe for bulk senders (5,000+/day thresholds, but treat it as required for everyone).
- **Never send from a free mailbox address** (name@gmail.com) — those domains publish DMARC policies that cause other providers to reject or junk the mail. Use name@theirbrand.com.
- Before creating any campaign, verify the sender is authenticated (via auth/domain status checks) instead of letting the send fail or land in spam.

## Consent Quality

- **Double opt-in** (confirmation email before the subscriber becomes active) yields smaller but dramatically healthier lists, and is effectively required for German/Austrian audiences. Recommend it by default for new forms; single opt-in is acceptable for low-risk contexts (existing customers, paid signups).
- Imported lists must be permission-based and recent. Ask when and how the addresses were collected. Addresses older than ~2 years without any sending are a bounce/spam-trap minefield — recommend a re-permission campaign or a list-cleaning service before mailing them.
- **Purchased, scraped, rented, or "borrowed" lists are never acceptable.** They contain spam traps, generate complaints, violate GDPR/CASL, and get accounts suspended. Decline and explain — no exceptions.

## Warm-up (new domains and new accounts)

Mailbox providers distrust sudden volume from an unknown domain. For a new sending domain or a list new to MailerLite:

1. Start by sending to the most engaged segment only (recent openers/clickers, recent customers).
2. Roughly double the audience every few sends *if* metrics stay healthy (bounces < 2%, complaints < 0.1%).
3. Reach full list volume over 2–4 weeks depending on list size. Small lists (< 5,000) can move faster.
4. Keep content consistent during warm-up; avoid link-heavy or image-only emails.

## List Hygiene and Sunset Policy

- MailerLite automatically suppresses hard bounces, unsubscribes, and complaints — never manually re-activate these statuses.
- Run a **sunset policy**: subscribers with no engagement in 90–180 days go through a re-engagement flow (see `automation-playbooks.md`); non-responders get moved to a suppressed group or unsubscribed. Mailing dead addresses forever is how domains end up in the spam folder.
- Watch soft bounces: an address that soft-bounces repeatedly across campaigns is effectively dead — clean it.
- Shrinking list + rising click rate = success, not failure. Say this to users worried about unsubscribes; the subscribers who leave were already gone.

## Content Factors

Content matters less than reputation, but still matters:

- Balanced text-to-image ratio; never image-only emails (invisible to text-only clients, classic spam signature).
- No URL shorteners (bit.ly etc.) — heavily abused by spammers, heavily penalized by filters.
- Link domains should match the sending domain where possible.
- Avoid spam-pattern language stacking: it's the combination (ALL CAPS + FREE + !!! + money emoji) that triggers filters, not single words.
- Include a plain-language footer: who is sending, physical address, working unsubscribe.

## Diagnosing Problems

| Symptom | Likely cause | Action |
|---|---|---|
| Sudden open-rate drop across whole list | Spam-folder placement | Check complaint/bounce rates on recent sends; pause volume; send next campaign to most-engaged segment only |
| High hard bounces on a send | Old or imported list | Stop; clean the list before the next send |
| High complaints (> 0.1%) | Audience didn't expect the email | Review consent source and frequency; tighten targeting |
| Low opens at one provider only (e.g. all Outlook) | Provider-specific reputation | Reduce volume to that provider's engaged users; check authentication |
| Unsubscribe spike | Frequency or relevance shift | Compare against recent sends; survey or segment |

Recovery is always the same medicine: cut volume to the engaged core, keep bounces/complaints pristine for several weeks, and expand gradually — reputation heals slowly.
