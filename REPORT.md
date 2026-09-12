# Benable Onboarding Review — Final Report

**Prepared for:** Julia Guillemot · **By:** Willa · **Date:** 2026-09-03
**Method:** Secret-shopper audit. Fresh account **Willa Skydive** (willa@skydivemail.ai, @willaskydive) created 2026-08-28 14:41 UTC via the web email-signup path (Paris IP). Inbox was empty at baseline, so every email below is attributable to Benable. Inbox swept 3×/day through 2026-09-03 07:00 UTC (~5d16h window). All emails opened, all CTAs and flows exercised (survey completed, dashboards verified via magic links, Wrapped viewed).
**Supporting files (same folder):** `email-log.md` (full raw log), `screenshots/` (signup flow b1–b21, survey1–6, email dashboards, Wrapped slides), `competitor-onboarding-research.md` (sourced comparison research).

---

## 1. Executive summary

Benable's week-one onboarding is **behaviorally sophisticated but executionally sloppy**. The architecture is genuinely strong — nearly every email is trigger-based rather than calendar-based, the $5 survey and tune-up dashboard are best-in-class activation mechanics, and the monthly Wrapped is a retention/viral idea most competitors don't have. But the sequence is undermined by a dense layer of template bugs (a raw `{user.contact_name_or_name}` variable in a day-1 email, full-name greetings on every automated email, "© 2025" footers, four separate copy typos), two structural gaps vs. every comparable platform (**no email verification** and **no day-2/3 re-engagement email for users who don't act**), and a premature referral ask in the first minute of the relationship.

**Top 5 fixes by impact-to-effort:**
1. Fix the raw template variable in the referral email (day-1, every new user sees it).
2. Switch all support@ templates from full name to first name (one merge-field change; the human-sender template already does it right).
3. Update "© 2025" → dynamic year across the template family.
4. Add email verification — ideally Linktree-style "verify to activate," or lean into the existing magic-link infrastructure and go passwordless.
5. Move the referral email from minute-2 to post-first-value (e.g. after first rec or first cashback), matching what every comparable platform does.

---

## 2. Complete email inventory (10 emails, 6 days)

| # | Timing (from signup) | Received (UTC) | Sender | Subject | Type / trigger |
|---|---|---|---|---|---|
| 1 | T+2 min | 08-28 14:43 | support@ (Benable Team) | "Hey!" | Welcome (signed Maria, Community lead); 90-sec video, magic-link login, FAQ/tutorials |
| 2 | T+2 min | 08-28 14:43 | support@ | "🙌 Refer a friend, you'll both earn higher commissions!" | Referral push (same minute as #1) |
| 3 | T+15 min | 08-28 14:56 | support@ | "Get your Benable lists discovered!" | Behavioral: first rec added → Optimized-badge education |
| 4 | T+25h | 08-29 16:02 | support@ | "Quick question = $5 for you!" | Incentivized signup-source survey (3 Qs, <1 min) |
| 5 | T+25h24m | 08-29 16:05 | support@ | "Bonus received!" | Transactional: $5 survey bonus credited (~1h after survey completion) |
| 6 | T+58h | 08-31 00:17 | support@ | "Your My favorite beauty recs list has been viewed!" | Behavioral: real-time list-view notification |
| 7 | T+62h | 08-31 04:53 | support@ | "People liked your Benable recommendations this week!" | Weekly like digest (n=1) |
| 8 | T+74h | 08-31 16:42 | **hannah.stevens@** (human) | "Get featured?" | Lifecycle: featured-list invitation, plain-text 1:1 style |
| 9 | T+76h | 08-31 18:27 | support@ | "Action-needed: suggestions to improve your list and profile quality!" | Lifecycle: Tune-up dashboard nudge (6 improvement items) |
| 10 | T+4d18h | 09-02 08:23 | support@ | "Your Aug '26 Benable Wrapped is ready!" | Monthly recap: 6-slide shareable Wrapped story |

**Cadence shape:** day-1 burst (3) → day-2 survey + bonus (2) → day-3 engagement notifications (2) → day-4 human outreach + tune-up (2) → day-5 Wrapped (1) → days 6+ silent. Total 10 emails in 5 days — heavier than Notion's documented 7-in-8-days and roughly Pinterest-tier, but note that ~half were triggered by *my* activity (recs added, survey done, list viewed/liked). A passive signup would have received meaningfully fewer — which is exactly the segment with no re-engagement coverage (see §5).

---

## 3. In-product flow observations (signup, 2026-08-28)

- Email signup: Full Name / Email / Password — **no email verification step anywhere**; the account is live immediately and no confirm-your-email is ever sent.
- **Invite-code step:** skippable — but skipping still produced "**Benable** invited you to join Benable!" and granted the 10% commission bonus for 30 days (house-account fallback). The exclusivity framing ("were you referred?") is undermined if everyone gets the bonus anyway.
- Phone-number step (skippable), username reservation, then a well-designed first-rec composer: geo-aware placeholder suggestions (Paris IP → "Crêpes Parisiennes"), auto-built product card, add-note step, confetti celebration.
- "Not just for products" step pushes a local/restaurant rec — good category education.
- Strong overall: the flow gets a user to 2 recs and a list before they ever reach the feed. This is a genuinely good activation funnel; the issues are polish, not architecture.

## 4. Bugs and defects found (by severity)

**High visibility / embarrassing:**
1. 🐛 **Raw template variable in Email 2:** greeting renders as "Hi, `{user.contact_name_or_name}`!" — a day-1 email every new user receives. Highest-priority fix in this report.
2. 🐛 **"FIRST REC" celebration repeats:** adding a *second* rec re-triggers "WOOHOO! YOU ADDED YOUR FIRST REC!".
3. 🐛 **Full-name greeting on every support@ email:** "Hi Willa Skydive" on emails 1, 3, 4, 5, 6, 7, 9, 10. Email 8 (human sender template) correctly says "Hi Willa," — proving the data is fine and the bug is in the support@ template family's merge field.
4. 🐛 **Stale "© 2025" footer** on every support@ email, now well into 2026.

**Copy/template defects:**
5. "your your list(s)" doubled word (Email 6); also non-pluralization-aware "list(s)".
6. "to take easily take action" garbled phrase (Email 9).
7. bit.ly slug typo `benable-optimsed-list-guidelines` ("optimsed"), used in Emails 3 and 8.
8. Stray orphan word "list" above the footer in Email 3 (broken template fragment).
9. Missing comma after greeting in several support@ emails.

**Product/UX issues surfaced by the audit:**
10. **"Top 80% most active users"** in Wrapped is statistically hollow (excludes only the bottom 20% — nearly everyone "achieves" it). Shareable by design, so it invites public ridicule à la the "top 91% of listeners" memes. Use a real percentile or suppress for low-activity accounts.
11. **"4.4 engagement score"** (Wrapped) has no scale, no explanation, and exists nowhere else in the product. Same problem as Email 9's "profile score" vs. the dashboard's "profile quality" — internal metrics leaking to users with inconsistent vocabulary.
12. **Email 5 never states the bonus amount or reason** ("you just received a cash bonus") — user must click through to learn it's $5 for the survey. Stating it would boost clarity and delight.
13. **Emails 6+7 double-notify one event:** a single visitor's single session (Marissa Everett viewing + liking one list) generated both a real-time view notification and a weekly "people liked" digest ~4.5h apart. Digest with n=1 feels thin; overlap will feel spammy at scale.
14. **Email anonymizes the viewer ("Someone in Peoria, IL") but the dashboard fully identifies her** (name, photo, timestamp). Privacy question: are viewers told their browsing is visible by name to list owners?
15. Email 9's tune-up count pads "install the mobile app" as one of "6 opportunities to improve your lists and profile quality" — it isn't one.
16. Email 8's "get featured" flattery is followed 1h45m later by Email 9's "your profile has 6 problems" — sequencing collision.
17. Email 4 subject says "Quick question" (singular) vs. body "3 quick questions" — minor.
18. Weekly digest sent 04:53 UTC Sunday (~midnight US Eastern) — batch job, not send-time-optimized.

**Security/compliance notes:**
19. **Magic-link tokens granting full login sessions sit in plaintext in every email.** Standard for the pattern, but each email is effectively a session credential — forwarding one forwards account access. Worth a deliberate policy review (expiry, single-use).
20. **No unsubscribe link in the plain-text part** of the Wrapped email (verified against the stored message: footer has only copyright + postal address). If the HTML part also lacks it, that's a CAN-SPAM/GDPR problem for a marketing email; even if HTML has it, plain-text readers get none.
21. Wrapped pages are public by URL token — intentionally shareable, but the URL exposes name + activity to anyone holding the link.
22. **No email verification at signup** (see gaps below) — accounts can be created with any address, which also means all these magic-link session emails could be delivered to an address the signer-up doesn't control.

## 5. Gaps vs. comparable platforms

Full research (sourced) in `competitor-onboarding-research.md`; benchmarks: LTK, ShopMy, Linktree, Pinterest, Substack, Notion, Duolingo.

| Dimension | Benable today | Comparable platforms |
|---|---|---|
| **Email verification** | None, at any point | Pinterest & Linktree: dedicated day-1 verify email (Linktree frames it as "activate your Linktree"); Substack & Notion: passwordless by design; ShopMy/LTK: gated by emailed approval/code. Only Duolingo skips it. |
| **Day-2/3 nudge for inactive users** | None observed — everything after day 1 was triggered by *my* activity. A passive signup gets the day-2 survey and then likely silence. | Duolingo's day-3 streak-freeze "recovery" email targets day-2 no-shows; Notion pulses 2/1/1/0/0/1/0/1 with feature-adoption emails regardless of activity; Pinterest sends interest-based content days 1–2 before the user does anything. |
| **Referral timing** | Minute 2 of the relationship (Email 2), before any value moment | **None of the six platforms asks for referrals in week one.** Referral literature is unanimous: fire after the first value moment. |
| **Sequence transparency / sender consistency** | Mixed senders (support@ "Benable Team", "Maria" signature, then hannah.stevens@); no series framing | Notion: numbered "(X/7)" series from one consistent human sender ("Zoe at Notion") |
| **Content-as-onboarding** | Emails are about features/mechanics; none show actual recommendations from the platform | Pinterest's activation emails *are* the product — curated Pins matched to signup interests, then your-own-board-based digests |
| **Single activation metric** | Diffuse: recs, badge, referral, survey, tune-up, app install all compete | LTK: Shop live; Linktree: page shared; Pinterest: first board; Notion: first doc — every email serves one goal |
| **Volume** | 10 in 5 days for an active user (day-1 burst of 3, incl. 2 in the same minute) | Notion 7-in-8; industry default 4–6 in week one, front-loaded then deliberately quiet mid-week |

**What Benable does that competitors don't (worth keeping and building on):**
- **$5 incentivized signup-source survey** with instant credited reward — flawless end-to-end, low friction, feeds segmentation. None of the compared platforms does this.
- **Tune-up dashboard** with per-item fixes and a progress ring — a genuinely good gamified quality loop (fix the email copy driving to it).
- **Monthly Wrapped** — on-trend, uses real user data, built-in share loop. Fix the hollow stats and it's a standout.
- **Human "get featured" outreach on day 4** — named sender, first-name greeting, reply invitation; boosts reply rates and feels concierge (ShopMy-like touch).
- Magic-link CTAs everywhere = zero-friction re-entry (just needs the security policy review above).

## 6. Recommendations

**Fix now (template-level, low effort):**
1. Repair `{user.contact_name_or_name}` in the referral email.
2. First-name merge field across the support@ template family (copy the human-template's behavior).
3. Dynamic copyright year.
4. Fix the four copy typos (§4 items 5–8) and the "FIRST REC" repeat celebration.
5. State "$5 for completing your survey" in the bonus email.

**Structural (this quarter):**
6. **Add email verification** — best: merge it with activation ("Verify to activate your Benable") or go fully passwordless via the magic-link infra you already have.
7. **Move the referral email** to fire on a value trigger (first cashback, first list view, or Optimized badge) instead of minute 2. The day-1 slot it frees can carry the Optimized-badge education.
8. **Add a day-2/3 recovery email for users with zero recs** — Benable's current sequence only talks to users who are already active; the churn-risk segment hears nothing after day 1. A "here are 5 lists we think you'll love" (Pinterest-style, interest-matched from the survey answers) does re-engagement and content-as-onboarding in one email.
9. **Deduplicate engagement notifications:** suppress the weekly digest when its only content was already sent as a real-time notification; set a minimum n for digests.
10. **Pick one activation metric** (suggest: *first list reaches Optimized badge* — it already has education, a dashboard, and the featured-list reward attached) and audit every week-one email against it.

**Polish:**
11. Fix or suppress the Wrapped "top 80%" stat; define the engagement score or cut it; unify "profile score"/"profile quality" vocabulary.
12. Sequence guard so the human "get featured" email and the "6 problems" tune-up email can't land within a few hours of each other.
13. Add plain-text unsubscribe to marketing templates; review magic-link expiry/single-use policy; decide the viewer-identity privacy stance (email vs. dashboard inconsistency).
14. Send-time-optimize the weekly digest (currently ~midnight US Eastern on Saturday).
15. Reconsider the house-account fallback that grants the 10% referral bonus to users who skip the invite step — either make the bonus universal and drop the invite-code framing, or make it genuinely referral-only.

**Optional follow-up tests I can run on request:** reply to Hannah's "get featured" email and audit the human-response loop; verify HTML-part unsubscribe presence across all templates; run a second passive account (zero activity) to map exactly what an inactive user receives; test the mobile-app onboarding path.

---

*Every claim above is backed by the raw log (`email-log.md`), screenshots (`screenshots/`), and sourced competitor research (`competitor-onboarding-research.md`) in this folder.*
