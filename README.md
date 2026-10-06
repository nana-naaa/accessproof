# AccessProof

**AI review integrity for accessibility data people can trust.**

🔗 **Live prototype:** https://nana-naaa.github.io/accessproof/

Built by **Team Atlas** for EnAccess Maps, Challenge 2: AI-Powered Review Quality Checker.

---

## The problem

EnAccess Maps wants to reward community members for reviewing the accessibility of local venues, for example ten reviews for one voucher. Rewards bring more reviews, but they also bring:

- **Fabricated** reviews of places the reviewer never visited
- **Rushed** one-liners written just to hit the target
- **Low-effort** reviews like "looks accessible" that nobody can plan a trip around

For a person with disability, one wrong "step-free" review can mean a wasted trip. And no team can check every review by hand.

## The solution

AccessProof gives every review a **trust score out of 100**, so EnAccess only rewards contributions people can rely on.

| Component | Points | What it checks | AI? |
|---|---|---|---|
| Corroboration | 35 | Do other independent contributors report the same thing at this venue? | No, arithmetic |
| Provenance | 30 | Location at submission, time on the form, spacing between submissions | No |
| Photo evidence | 20 | Is the photo of this venue, and does it show what was recorded? | Vision model |
| Specificity | 15 | Does the note contain observable, checkable detail? | Language model |
| Contributor history | +10 bonus | A record of accepted reviews lifts the score. New contributors are never marked down | No |

- **70 or above:** publishes and counts toward the reward
- **40 to 69:** goes back to the contributor, asking for the one thing that scored lowest
- **Below 40:** held for a human
- **Hard gates:** submitting far from the venue, or many reviews in minutes, goes to a human whatever the score

Corroboration weighs most because it's the only check of whether a claim is *true*. Specificity weighs least so people who write briefly or type on a phone aren't penalised.

**Asymmetric thresholds.** A "step-free" claim needs 70 to publish; a "there is a step" claim needs 55. Wrongly calling a venue accessible strands someone at a door, which is worse than a missed visit.

**Cold start.** The first review of a venue has nothing to corroborate against, so its 35 points are spread across the other components. It publishes marked "reported by one visitor, awaiting a second", and still counts toward the voucher.

**Limits.** AccessProof makes faking cost more than a voucher is worth. It doesn't stop coordinated collusion; a cap on rewards per contributor handles that. The weights are a starting point, to be calibrated in month 1.

**AI drafts. People decide.** Instead of silently deleting weak reviews, AccessProof drafts a follow-up (clarification, photo request or short survey). A moderator with lived experience approves it before it's sent, in the reviewer's own language.

## What's in the prototype

A clickable council dashboard with four views:

- **Truth:** key metrics, AI weekly brief, flagged reviews and a hotspot map
- **Pulse:** live moderation feed for today
- **Trajectory:** how the average trust score improves over time
- **Actions:** AI-drafted, human-approved follow-ups in English, Chinese and Korean

> All figures and reviews are **demo data**. Scoring is not connected to a live model yet.

## Run it locally

It's a single HTML file with no install or build step. Download `index.html` and open it in any browser.

## Next steps

1. **Month 1:** co-design quality criteria with EnAccess and lived-experience reviewers; label past reviews
2. **Months 2–3:** build the scoring model and test it on labelled reviews
3. **Months 4–6:** pilot at one Mapping Day or council area and measure the results
