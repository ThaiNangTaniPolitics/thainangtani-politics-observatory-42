## 0077 – The Postbag Filter
### *How moderation, not authorship, produces the voices that survive Bangkok Post's letters forum*

-----

The Postbag letters section is pluralistic; the comment space beneath it is not. The difference is not produced by who writes — it is produced by a **retrospective, selective moderation that follows the *who*, not the *what*.** This node answers with measurement the question [0073](0073-where-the-comments-went.md) left open as a negative finding, and builds on the comment-ecology baselines of [0011](0011-bangkok-post-comment-ecology.md), [0027](0027-bangkok-post-discursive-Filtering-comment-section-2026.md) and [0053](0053-bangkok-post-institutional-discourse-distortion.md).

**Data basis (open `/comment/process` interface, own crawl July 2026).** ~2,500 surviving Postbag comments (March 2024–July 2026 — the *end state* after deletion; raw arrivals are gone); 3,021 printed letters across 855 pages by 608 authors; two ID-sweep windows (January + July 2026) of 1,500 comments outside the Postbag as a control. Tools: `bp_comments.py`, `postbag_letters.py`, `id_sweep.py`, `analyse_postbag.py`, `zensurquote.py`, `watch_counts.py`, `verlust.py`. **Calibration (load-bearing): every figure measures *survival*, not *arrival*. What was deleted is unrecoverable.**

## 1. The paper-wide comment volume — the quiet collapse

The `comment_id` is a **global counter for the whole paper** (news and Postbag IDs of the same day interleave), so its monthly increment measures total volume. From a steady ~78–112k/month through 2024, to a **spring-2025 peak of ~128k**, then a fall from mid-2025 to **~30–50k in 2026** (July 2026 ~29k): **a decline to roughly a quarter.** *Method note:* an April 2026 renumbering (a jump of +533 million) is skipped, and min–max IDs per day are used rather than a median (more robust). *The reading is held open:* the counter measures submissions; it does not separate fewer readers from harder moderation from platform fatigue.

## 2. The mode of moderation — retrospective and selective, not a pre-filter

This is the central clarification. Six findings fit together:

1. Comments appear **immediately, with real timestamps** (including ~7% posted overnight) → there is **no approval queue.**
2. They are **deleted within days**, then stable (an age curve; corroborated by the user's own record: published, then removed days later).
3. **Whole threads go together** (0 of 1,605 replies left orphaned) → the target's removal takes the attack with it.
4. The trigger is a **report, not a content scanner**: obscenity *by* the surviving cluster remains, while a factual characterisation *of* the cluster is deleted.
5. **Downvotes are not moderation**: −162 and −97 still stand.
6. **No prior review** (median reply lag 4.5–6h, never negative).

⇒ Moderation follows **whom**, not **what**. Left open (the data do not separate it): whether reports are filed by users or by the desk — the reporting mechanism is documented (Felix_Qui names it himself) and requires no editorial involvement. **No claim of "organised"** is made: coordination tests came back negative.

## 3. The deletion rate

About **87%** (July 2026, live counter, fresh-vs-settled pages in the same month): fresh pages carry 12.3 comments, settled pages 1.6. It happens within days, not over years — the *oldest* pages carry the *most* comments, so this is not archive housekeeping. A user tally of March 2025 (600 comments, by hand) is **unchanged 16 months later**, confirming "within days, then stable."

## 4. Seven documented deletions — the rule

**What is removed is the characterisation of the person, not the refutation of the point.** (Full table in the node-internal record.)

- **Survived:** substantive disagreement with a setter (+17/−7), factual rebuttal (+18/−2), off-topic (television +34/−1, sport +20/−1).
- **Deleted:** "reactionary, ideologically tinted," "redactional echo amplifier," "cold-hearted right-wing populist."

These are evidenced by the user's screen-captures of the *state before deletion* — independent of the crawl data.

<!-- §112-INTERNAL NOTE: royal-touching moderation cases (comments removed for referencing the monarchy/palaces) are held only in [[bp-moderation-royale-kommentare]] and NEVER surface in a public derivative. The public finding is the secular one: characterisation of a person is reportable and removed; the point it carried is not. -->

## 5. The cluster and the news counter-test

A few accounts (the Ima chain, the keskeseksa chain, Cryptic, Chris_Z, bkkmatt …) supply ~50% of the surviving Postbag stock, with a net-negative vote balance. Account *successions* are visible (keskeseksa → keskesaksa → Keskaseksa): the Post has no rename, so a new name is a new account and, the old name being taken, one letter is swapped (details in the actor dossier). **The news counter-test (two windows):** the same accounts there hold only **10–13%**, with a positive climate (+0.45/+0.61). ⇒ **It is not the actors, it is the selection inside the Postbag.**

## 6. Letters versus comments — the asymmetry

| | Letters (the desk chooses) | Comments (what survives) |
|---|---|---|
| strongest actor | Setter **7%** | one account ~20% |
| Top-5 / Top-20 | 27% / 50% | Top-5 = **56%** |
| one-time contributors | **65%** | 30% |

608 letter-authors, two-thirds appearing once → a **broad editorial selection**. The comment space is narrow → **narrowing by moderation, not by authorship.**

## 7. Setter as the hinge, and the January 2026 break

**Michael Setter** is the most-printed letter-writer (**218**, ahead of Burin Kantabutra 202 and Felix Qui 152) and the most-commented-on actor. His cadence of 6–14 letters/month through December 2025 falls to **1 in January 2026, 0 in February**, then 1–4. The **same January-2026 break appears in both series** — letters *and* surviving comments per page — so two independent sources corroborate each other (details in the Setter/caesura record).

## 8. The house rules that cover it (bangkokpost.com/terms, 1.1.1)

- (c) "threatens, defames or assaults other persons" → any characterisation of a person is reportable.
- (d) users must not "act as our Moderator" → **criticism of the moderation is itself a breach.**
- (e) "politics… King or the dynasty… or other nations" → wide enough to catch anything.

The Post deletes "but disclaims any obligation or responsibility," without giving a reason → the user's queries went unanswered (a term of business, not negligence). **The core is not rule-breaking but the *one-sided invocation* of a rule everyone falls under.**

## 9. What the data do NOT show (discipline)

Raw arrivals (only survival is measurable); who files the reports; whether the desk participates; whether the volume falls from moderation or reader attrition. **Rejected as metrics:** "sole survivors" and "median daily position" (they measure presence, or the hole left after deletion, not behaviour). **Cui bono is not proof.** A forward deletion measurement (`verlust.py`) is running.

-----

## Sources

**Own crawl, July 2026 (interface `/comment/process`); data preservation 2026-07-25** (`2026_ClaudeCode\BangkokPost\Postbag_Sicherung\20260725\`)

**bangkokpost.com/terms, section 1.1.1** (live + Wayback 1 June 2024)
https://www.bangkokpost.com/terms

**User screen-captures (OneNote) of the seven deletion cases — state before removal; user census March 2025**

-----

## Discipline checklist (verification record)

- [x] **Survival, not arrival.** Every figure is stated as measuring surviving comments; raw volume is explicitly unrecoverable and not claimed.
- [x] **Renumbering artefact excluded.** The April 2026 +533m ID jump is skipped; min–max-per-day used, not median.
- [x] **"Follows whom, not what" is evidenced, not asserted.** Six converging findings (immediate posting, days-later deletion, whole-thread removal, report-trigger, downvotes-stand, no prior review) support it; the report source (user vs desk) is left open.
- [x] **No "organised" claim.** Coordination tests negative; the reporting mechanism needs no editorial involvement.
- [x] **§112 quarantined.** Royal-touching moderation cases stay in the node-internal record; the public finding is secular (characterisation removed, point kept).
- [x] **Actors vs selection.** The news counter-test (10–13% vs ~50%) locates the effect in the Postbag selection, not the accounts; the cluster is named without an intent charge.
- [x] **Rules read as one-sided invocation, not breach.** The finding is selective enforcement of terms everyone falls under, not that the Post violated its own rules.

-----

*Filed under: Bangkok Post comment ecology, moderation, discourse filtering, media plurality*
*Cross-references: [0011 – BP Comment Ecology](0011-bangkok-post-comment-ecology.md), [0027 – Discursive Filtering](0027-bangkok-post-discursive-Filtering-comment-section-2026.md), [0053 – BP Institutional Discourse Distortion](0053-bangkok-post-institutional-discourse-distortion.md), [0073 – Where the Comments Went](0073-where-the-comments-went.md)*

<img src="../images/0077_1.webp" alt="0077_1" style="width: 480px; margin: auto;" loading="lazy">

<img src="../images/0077_2.webp" alt="0077_2" style="width: 480px; margin: auto;" loading="lazy">

