Project: Ocean Park 1 Eats — Aggregated Dining Info  
Owner: Cong Thai — Product Spec Owner  
Main responsibility: propose build slices, choose the final slice, define Auto/Aug decision, and describe four paths for the prototype.

---

## 1. Context

Residents of Ocean Park 1 often need to make a quick food decision, but information is scattered across Facebook groups, Google Maps, ShopeeFood, GrabFood, and informal user reports. The main pain is not simply “finding food”; the harder problem is knowing which option is reliable right now: open, available, close enough, and likely to deliver within the expected time.

For Day 06, the prototype should avoid overbuilding a full food-ordering app. The goal is to choose a narrow build slice that can be demonstrated with controlled fake data, visible confidence, and clear fallback behavior.

---

## 2. Prototype Assumptions

This file assumes the Day 06 prototype is a thin demo, not a production system.

- No live scraping.
- No real payment or order placement.
- No direct integration with ShopeeFood, GrabFood, Google Maps, or Facebook APIs.
- Data will be fake/controlled and stored in CSV or SQLite.
- The AI decision can be implemented as a simple ranking heuristic or lightweight LLM-assisted explanation over structured data.
- All restaurant names used in demo data must be replaced or verified by Member A/B before final submission.
- Any unverified restaurant name should be marked as `demo placeholder`.

Suggested minimum data fields:

| Field | Meaning |
|---|---|
| `restaurant_id` | Unique restaurant ID |
| `restaurant_name` | Restaurant name |
| `vendor` | GrabFood, ShopeeFood, direct order, pickup |
| `platform_eta_min` | Current/simulated ETA from food platform |
| `platform_eta_max` | Upper ETA estimate |
| `open_status` | open / closed / unknown |
| `recent_report_status` | normal / slow / cancelled / unknown |
| `report_recency_min` | How recent the user/community report is |
| `distance_score` | Simple score for distance from user location |
| `evidence_links` | Links or IDs to source evidence |
| `confidence` | high / medium / low |

---

## 3. Product Slices Exploration

### Slice A — Quick Open + Cuisine Finder

**User:**  
Resident of Ocean Park 1 who wants to know which restaurants are open within the next 30 minutes.

**Task:**  
Find 2–3 nearby restaurants that are likely open now and match a broad cuisine type.

**AI decision:**  
Infer `open_now_confidence` from simulated opening hours, recent community posts, and user reports.

**Output:**  
A ranked list of 3 restaurants with:

- open/unknown status
- cuisine type
- confidence level
- short reason
- source/evidence link

**Failure mitigation:**  
If confidence is low or sources conflict, the UI shows “Check before going” and suggests calling the restaurant or choosing another option.

**Why this slice is useful:**  
It addresses a common uncertainty: users do not know whether a place is actually open.

**Why not chosen for Day 06:**  
Open-now status can be risky without real-time verification. A fake-data demo may look useful, but the real-world value depends heavily on accurate live updates.

---

### Slice B — Fast Delivery Suggestion [CHOSEN]

**User:**  
Busy Ocean Park 1 resident who wants food delivered within about 30–45 minutes.

**Task:**  
Choose 1–2 restaurants that are most likely to deliver fast right now.

**AI decision:**  
Estimate expected delivery ETA and confidence from simulated delivery-platform ETA, recent resident reports, open status, and distance score.

**Output:**  
Two recommendation cards, each showing:

- restaurant name
- predicted ETA range
- confidence level
- short rationale
- evidence/source links
- fallback action: call, pickup, or choose alternative

**Failure mitigation:**  
The system never places an order automatically. It shows confidence and evidence before the user decides. If confidence is low, the system labels the result as “Check before ordering”.

**Why this slice is useful:**  
It solves a narrow, frequent, and demo-friendly problem: users want food quickly but do not trust ETA signals across platforms.

**Why chosen for Day 06:**

1. **Narrow user task:** “I want fast delivery now” is specific and easy to demo.
2. **Clear AI decision:** predict ETA and confidence, then rank options.
3. **Easy fake data:** ETA, recent reports, and open status can be simulated in SQLite.
4. **Visible value:** users immediately understand the output: 2 options, ETA, confidence, and reason.
5. **Good failure path:** wrong ETA or closed restaurant can be handled through report/correction flow.

---

### Slice C — Dietary Filtered Suggestion

**User:**  
Resident or visitor in Ocean Park 1 who needs vegetarian, halal, or other dietary-specific food options.

**Task:**  
Find restaurants that likely match the dietary constraint.

**AI decision:**  
Classify restaurants by dietary tags using simulated menu tags and community evidence.

**Output:**  
Top 3 restaurants with:

- dietary tag
- confidence level
- menu/evidence snippet
- warning if evidence is weak

**Failure mitigation:**  
If the source evidence is unclear, the system shows “Needs verification” and asks the user to check the menu or contact the restaurant.

**Why this slice is useful:**  
It supports users with stricter food constraints and reduces manual searching.

**Why not chosen for Day 06:**  
Dietary claims are higher-risk and harder to validate in a short prototype. A wrong halal/vegetarian tag can harm trust more seriously than a wrong ETA estimate.

---

## 4. Final Build Slice

Chosen slice: **Slice B — Fast Delivery Suggestion**

### One-sentence build slice

For busy Ocean Park 1 residents who want food delivered within about 45 minutes, the prototype ranks nearby restaurant options using simulated ETA and recent delivery reports, then shows 2 recommended options with confidence, evidence, and fallback actions.

### User

Busy resident in Ocean Park 1 who is hungry, does not want to compare multiple apps, and wants a quick delivery decision.

### User task

Find food that can probably arrive within 30–45 minutes.

### AI decision

Predict which restaurants are most likely to deliver fastest right now.

### Human decision

The user chooses whether to order, call, pickup, or ignore the recommendation.

### Output

Two restaurant cards:

```text
Restaurant: [Name]
Predicted ETA: [30–40 min]
Confidence: [High / Medium / Low]
Reason: [Recent ETA stable + no slow reports]
Evidence: [Grab ETA / ShopeeFood ETA / user report]
Action: [View menu] [Call] [Pickup option]
```

---

## 5. Auto / Aug Decision

### Decision

**Augmentation, not full automation.**

### AI role

The AI assists the user by:

- estimating ETA range
- ranking restaurant options
- assigning confidence level
- explaining the ranking using evidence
- warning when data is conflicting or weak

### Human role

The user remains in control by:

- reviewing the suggestion
- checking confidence and evidence
- deciding whether to order
- choosing fallback actions when uncertainty is high

### Boundary

The AI must not:

- place an order automatically
- hide uncertainty
- recommend low-confidence options as if they are reliable
- claim real-time accuracy when the data is simulated or stale

### Why this decision is appropriate

Fast delivery is a moderate-risk decision. A wrong recommendation can waste time, cause frustration, or lead to a failed order. Therefore, the prototype should support the user’s decision instead of replacing it.

---

## 6. Ranking Logic for Prototype

This is a simple heuristic suitable for Day 06. It is not a production model.

### Inputs

- `platform_eta_min`
- `platform_eta_max`
- `open_status`
- `recent_report_status`
- `report_recency_min`
- `distance_score`
- `evidence_count`

### Basic ranking rule

A restaurant ranks higher when:

- it is open or likely open
- ETA is lower
- recent reports are normal
- there are no cancellation/slow-delivery reports
- distance score is favorable
- evidence is recent and not conflicting

### Confidence rule

| Condition | Confidence |
|---|---|
| ETA is consistent across sources, open status is clear, no bad recent reports | High |
| Some evidence is missing, but no strong conflict | Medium |
| ETA conflicts, open status unknown, or recent slow/cancelled reports exist | Low |

### Example pseudo-logic

```text
if open_status == "closed":
    exclude or mark unavailable

if recent_report_status in ["cancelled", "very_slow"] and report_recency_min <= 60:
    confidence = "low"

predicted_eta = weighted_average(platform_eta_min, platform_eta_max, recent_report_eta)

rank_score = eta_score + distance_score + evidence_score - conflict_penalty
```

---

## 7. Four Paths for Slice B

### 7.1 Happy Path

**Trigger:**  
User selects “Giao nhanh” during a normal time window.

**Input condition:**

- Restaurant is open.
- Grab/ShopeeFood ETA is around 30–40 minutes.
- No recent complaint about delay or cancellation.
- Evidence is recent enough.

**System behavior:**

- Query fake SQLite dataset.
- Rank restaurants by predicted ETA and confidence.
- Return 2 best options.
- Show evidence links and short rationale.

**User control:**

- User opens menu or external delivery app.
- User makes final order decision.

**Output example:**

```text
Option 1: Demo Restaurant A
Predicted ETA: 30–40 min
Confidence: High
Reason: ETA stable across sources; no slow reports in the last 60 minutes.
Action: View menu / Order via app / Call
```

**Logged data:**

- query type: fast_delivery
- selected option
- confidence shown
- evidence shown

---

### 7.2 Low-confidence Path

**Trigger:**  
User searches for fast delivery, but data sources conflict.

**Input condition:**

- GrabFood ETA says 25 minutes.
- ShopeeFood ETA says 50 minutes.
- Recent community report says delivery is slow due to rain, peak hour, or lack of drivers.

**System behavior:**

- Do not hide the restaurant automatically.
- Lower confidence to LOW.
- Show ETA as a range, for example 45–60 minutes.
- Explain the conflict in plain language.
- Recommend a safer alternative if available.

**User control:**

- User can still order.
- User can call the restaurant.
- User can choose pickup.
- User can pick another recommendation.

**Output example:**

```text
Option 1: Demo Restaurant B
Predicted ETA: 45–60 min
Confidence: Low
Reason: Platform ETA conflicts with recent resident reports about slow delivery.
Warning: Check before ordering.
Actions: Call restaurant / Choose pickup / See alternative
```

**Logged data:**

- conflict_type: eta_mismatch
- confidence: low
- fallback shown: true

---

### 7.3 Failure Path

**Trigger:**  
AI predicts fast delivery, but the real outcome is bad.

**Failure example:**  
The system predicts ETA 30–40 minutes with high confidence, but the user later reports that the order was cancelled, the restaurant was closed, or delivery took more than 60 minutes.

**System behavior:**

- User clicks “Report wrong ETA” or “Report closed/unavailable”.
- System records the mismatch.
- The restaurant is temporarily down-ranked in the current demo/session.
- The UI shows fallback options.

**User control:**

- User can choose another restaurant.
- User can switch to pickup.
- User can call the restaurant.
- User can submit correction evidence.

**Output example:**

```text
Sorry, this recommendation may be wrong.
Reported issue: Delivery delayed over 60 minutes.
Suggested next step: Choose a nearby pickup option or try another high-confidence restaurant.
```

**Logged data:**

- failure_type: wrong_eta / closed / cancelled
- predicted_eta
- actual_user_report
- restaurant_id
- timestamp

---

### 7.4 Correction Path

**Trigger:**  
User notices that restaurant information is wrong.

**Correction examples:**

- Restaurant is closed.
- Hotline is wrong.
- Menu is outdated.
- Delivery is currently unavailable.
- Location changed.

**System behavior:**

- Show a short correction form.
- Let user choose the error type.
- Let user add optional note or screenshot link.
- Temporarily mark the restaurant as “Needs verification”.
- Create a review item for Evidence Owner.

**User control:**

- User decides whether to submit correction.
- User can continue using recommendations without submitting.

**Output example:**

```text
Thanks for the correction.
This restaurant will be marked as “Needs verification” until the team checks the evidence.
```

**Logged data:**

- correction_type
- user_note
- restaurant_id
- source_conflict
- needs_review: true

---

## 8. Worst Failure Mode

### Worst failure

The AI recommends a restaurant as fast and available, but the restaurant is actually closed, unavailable, or delivery is suspended.

### Impact

- User wastes time.
- User may place a failed order.
- User loses trust in the product.
- The product appears to “invent certainty” from weak data.

### Prototype mitigation

The prototype handles this by:

- always showing confidence
- always showing evidence/source links
- never auto-ordering
- marking uncertain recommendations as “Check before ordering”
- providing fallback actions: call, pickup, or alternative restaurant
- allowing user correction
- logging mismatch for evidence review

### Rule

If confidence is low, the system must not present the option as “recommended”. It should present it as “possible option — check first”.

---

## 9. Handoff to Prototype Owner

Member D can build a thin prototype using this flow:

1. User opens app.
2. User selects “Giao nhanh”.
3. User location defaults to Ocean Park 1.
4. Backend reads fake restaurant data from SQLite.
5. Ranking heuristic calculates ETA and confidence.
6. UI shows 2 recommendation cards.
7. User can click:
   - view source
   - call restaurant
   - report wrong info
   - see alternative

Minimum screens:

1. Search/input screen
2. Recommendation results screen
3. Low-confidence warning state
4. Report/correction form
5. Fallback alternative state

---

## 10. Success Criteria

For Day 06, the build slice is successful if:

- The prototype returns 2 recommendations from fake data.
- Each recommendation includes ETA, confidence, reason, and evidence.
- The happy path can be demoed in under 3 minutes.
- Low-confidence path visibly shows uncertainty.
- Failure path allows user to report wrong ETA or closed restaurant.
- The system never claims to place an order automatically.
- The team can explain why Slice B was chosen over Slice A and Slice C.

---

## 11. Out of Scope

The following are not part of this build slice:

- Full food ordering flow
- Payment
- Live scraping
- Real-time delivery API integration
- Complete restaurant discovery app
- Full dietary verification system
- Long-term trust/reputation model
- Production-grade recommendation model

---

## 12. Final Summary

Slice B is the best Day 06 build slice because it is narrow, testable, and demo-friendly. It focuses on one user, one task, one AI decision, and one clear output. The AI does not replace the user’s judgment; it helps the user make a faster and more informed food-delivery decision by ranking options, showing confidence, and exposing uncertainty.
