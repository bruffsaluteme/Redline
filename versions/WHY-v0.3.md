# WHY v0.3

Built from `REDLINE-v0.3-brief.md` (prepared 2026-08-11 from a 1,112-trip corpus,
Apr 1 – Aug 1 2026, plus 13 weekly earnings summaries covering 649.3 online hours).

v0.2.3 is preserved byte-for-byte at `versions/index-v0.2.3.html` (15,716 bytes).

---

## What the "broken metric" turned out to be

The brief reported that `per all-in hour` "never shows a value" and suggested the code
might be producing `Infinity` or `NaN` from an empty Minutes field. It flagged the
diagnosis as unverified and asked that the calculate function be read first.

**It was read, and then tested in a browser. The premise does not hold.**

v0.2.3 line 305 already guarded the division:

```js
$('s2').textContent = (isFinite(T) && T>0) ? money(F/(T/60)) : '—';
```

Measured behaviour of v0.2.3, fare $113.13 / 106.7 miles:

| Minutes | Tile showed | Correct? |
|---|---|---|
| blank | `—` | guard working |
| 220 | `$30.85` | yes — 113.13 / (220/60) |
| 0 | `—` | guard working |
| 90 | `$75.42` | yes — 113.13 / (90/60) |

No `NaN`, no `Infinity`, no console errors. The arithmetic was never broken.

**The actual defect is that the tile never says what it wants.** Minutes was labelled
*optional*, so there was no reason to fill it, and the tile sat at `—` looking like a
dead readout rather than a waiting one.

**Second cause, not in the brief:** in **Last-ride mode the hourly metric does not
exist**. That tile is reused for `per paid mile`. Anyone working mostly in Last-ride
would never see an hourly figure under any input — which fits the "never" in the
original report better than the Minutes explanation does.

---

## Changed in v0.3

| Change | Why |
|---|---|
| Tile label swaps to *"add minutes to see this"* when Minutes is empty or zero | Fix (b) from the brief. The number explains itself instead of sitting blank. |
| Minutes relabelled *"needed for the hourly figure"* (was *"optional"*) | Root cause. The field was labelled as skippable, so it got skipped. |
| Division guard kept and commented | Was already correct; now it is obvious why it is there. |
| Cost-per-mile relabelled *"fuel + basic wear only"*, with `$0.32–0.45` disclosed on screen | Task 3. Defaults unchanged, as instructed — but the screen no longer implies $0.18 is the true all-in cost. |

---

## Deliberately NOT changed, and why

**Thresholds are untouched** — still `red < $0.55 | thin < $0.75 | pays < $1.10` per
total mile.

The brief was explicit that the corpus percentiles are **per paid mile** while Redline
scores **per total mile**, that deadhead was never recorded, and that the implied
`~$1.00` figure is "a direction to investigate, not a number to ship". Shipping any
recalibrated number would mean inventing the deadhead ratio the corpus cannot supply.

**Thresholds are not yet split by direction.** The brief recommends splitting
outbound / inbound / local and says this is safe because it can be "driven by the mode
toggle already in the UI". The existing toggle is **Mid-shift / Last-ride** — that is
*when in the shift*, not *which direction the trip runs*. The two are independent: an
outbound airport run can be either. There is no direction control in the UI to drive
the split, and the per-direction thresholds would still need total-mile units the
corpus cannot produce. Splitting requires both a new control and a defensible number.

**No "full cost" mode.** The brief suggests one, but the true all-in figure is a
$0.32–0.45 estimate precisely because insurance, car payment, purchase price and
depreciation were never entered. A default picked from that range would be an invented
number wearing a precise label. Disclosed as a range on screen instead.

**No airport copy correction was needed.** The brief asks that any copy implying
airport rides are a losing play be corrected. The app was searched: the only airport
references are the Bay City / Wayne comparison, which makes a long-haul-versus-short-hop
point, not an airport-versus-local one. Nothing in v0.2.3 claims airport rides lose
money, so there was nothing to reverse.

---

## Version lineage

| Version | Math changed | Why it exists |
|---|---|---|
| v0.1 | — | first build, three inputs. Charged every empty mile as lost earnings. |
| v0.2 | **yes** | added Mid-shift / Last-ride. Also shipped broken: a doubled backslash killed the script. |
| v0.2.1 | no | safety warning moved out of the README onto the screen. |
| v0.2.2 | no | "clean finish" read like permission. Now says it scores cash only. |
| v0.2.3 | no | Calculate button, `<noscript>` warning, redundant bindings. |
| v0.3 | no | hourly tile explains itself; Minutes no longer labelled optional; cost-per-mile relabelled as fuel + basic wear with the real range disclosed. **Thresholds unchanged pending the deadhead question.** |

---

## Still open

- Deadhead ratio: needed before any threshold move. The corpus cannot supply it.
- Direction split: needs a direction control, and thresholds in total-mile units.
- iPhone Safari test before this goes to the first outside user.

**Published ≠ finished. Not done until it has been handed to the intended first user.**
