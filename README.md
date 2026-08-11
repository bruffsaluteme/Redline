# Redline

**One small tool for rideshare drivers, built from one driver's own trip data.**

### **[→ Open Redline](https://bruffsaluteme.github.io/Redline/)**

*v0.2.3 · early field test · free, nothing to install, works offline once loaded*

---

## The $143 ride that lost to the $18 ride

I picked up at Detroit Metro and drove to Bay City. **$143.41.** Best fare I'd seen in a while — 117 paid miles, a $24.59 tip, and it felt like the day was made.

Another night, DTW to Wayne. **$18.28.** Six miles. Barely worth logging.

Then I put both through the only number that actually matters — dollars per mile I *drove*, not miles I got *paid* for. Bay City is 110 miles from Detroit, and nobody's catching an Uber out of there at eleven at night. So that ride was really 228 miles of car.

| Ride | Fare | Per paid mile | Per mile actually driven |
|---|---|---|---|
| DTW → Bay City | $143.41 | $1.22 | **$0.63** |
| DTW → Okemos | $83.22 | $1.03 | **$0.53** |
| DTW → Wayne | $18.28 | $3.09 | **$1.53** |

The $18 ride beat the $143 ride by **two and a half times.**

The app pays you for the miles with somebody in the car. Your gas, tires, brakes and resale value don't know the difference.

So I built this.

---

## How to use it

Fare, trip miles, and how far you'll drive empty afterward. Tap **Calculate** — or it updates as you type. It tells you what the ride pays per mile you actually drive, and whether it's in the red.

The field people ask about is **empty miles after**. It's one question:

> After you drop them off, how far do you drive before somebody's paying you again?

Back to the airport, over to a busier area, or **zero** if a ride's already waiting. Hit *ride waiting* and watch Bay City go from $0.63 to $1.22.

That's the real lesson in the tool. The number isn't about the ride. **It's about what you do after it.**

### Two modes, because the same ride isn't worth the same at 3pm and at 11pm

**Mid-shift** — you're staying out. Every empty mile is a mile you could have been earning, so the fare gets spread across the whole distance.

**Last ride** — you're going home after this one. There's nothing left to earn, so the empty drive isn't costing you fares. It's costing you gas and wear. This mode subtracts what the drive actually costs and shows you **what you keep**.

Same trip, both ways — a $113.13 airport run, 106.7 miles out, 106.7 back:

| Mode | Result |
|---|---|
| Mid-shift | $0.53 per total mile — **in the red** |
| Last ride, hybrid ($0.18/mi) | drive costs $19.21, **you keep $93.92 — 83%** |
| Last ride, gas car ($0.28/mi) | drive costs $29.88, you keep $83.25 — 74% |

Same fare. Same miles. Opposite answers. **The slot changed.**

It re-scores old rides too. That $143 Bay City run is thin as a mid-shift ride and an **85% clean finish** as a closer. It may have been a fine ride taken at the wrong hour.

**Set your cost per mile honestly.** A hybrid runs about $0.18, a gas car closer to $0.28. It changes the verdict. Those are estimates, not facts about your car.

---

## Use it parked

**Check a ride before you accept it, or after you drop off. Not while you're moving.** The tool says so on screen. Your job is driving; this is for the minute before or after.

## How it works

- No account, no signup, nothing to install
- **Nothing you type leaves your phone.** There's no server to send it to and no analytics. I can't see your numbers.
- Works with no signal once the page has loaded
- On iPhone: Share → **Add to Home Screen** and it opens like an app

### A note on saving the file
**Open it from the link above, not from a downloaded file.** If you save `index.html` and open it from your phone's Files app, iOS shows a flat preview that doesn't run the page — nothing will calculate. That's a limitation of the preview, not the tool. Use the link, or add it to your Home Screen.

---

## Where the numbers came from

Real trips, read off the Uber app, from one driver working Detroit Metro. Airport runs, downtown short hops, out-of-state reservations, June and July 2026.

The thresholds are calibrated to that data:

| Per mile actually driven | Verdict |
|---|---|
| under $0.55 | in the red |
| $0.55 – $0.75 | thin |
| $0.75 – $1.10 | it pays |
| over $1.10 | take it |

**Which means they might be wrong where you drive.** One market, one driver, one hybrid Camry. If your break-even is different, that's the most useful thing you could tell me — **open a Discussion** and say so. Getting corrected is the point of publishing this early.

---

## What this tool doesn't do

- **The empty drive is your estimate, not a measurement.** Good enough to rank rides against each other. Not a precise rate.
- **Mid-shift mode has no fuel or depreciation math.** It compares rides to each other. Only last-ride mode uses your cost per mile, and only for the drive home.
- **It doesn't include insurance, depreciation, financing, or taxes.** My own measured fuel cost is about 9 cents a mile. Real all-in cost is closer to 32–45 cents. This is not a profit calculator.
- **It doesn't know about surge, boosts, or promotions.** Those change the fare — put the real number in.
- **It won't tell you whether to drive.** Only whether *this* ride beats the alternative in front of you.
- **It doesn't know why you stopped.** If a gap was a restroom break, a phone call, or a meal, that isn't waiting — the tool can't tell the difference.
- **There's no break mode, on purpose.** A break isn't a ride, and the moment a tool starts asking what you were doing it stops being usable in fifteen seconds. Labelling breaks is a job for reviewing a whole shift afterward.
- **Last-ride mode prices the car, not the clock — and this is the one to watch.** A "clean finish" means the fare survived the drive home. It is **not** a recommendation to take the ride. A big late haul can keep 85% of its money and still cost you the next morning, and the tool has no way to see that. It scores cash. The hour is your call.
- **No guarantee of profitability.** This is an educational decision-support tool. You're responsible for your own driving, your own safety, and following your platform's rules.

---

## Why I made it

I drive to pay the bills, and I've been teaching myself to build things out of my own data instead of guessing. This came out of that. Every rule in here started as something I noticed on a shift and only later proved with numbers.

One question behind all of it:

**What did that actually pay me?**

If you drive, try it and tell me where it's wrong.

---

## Status and license

**Early field test — v0.2.3.** Expect the thresholds to move as drivers report back. A companion tool for airport queue-wait decisions exists but is deliberately unreleased until this one has been used by somebody other than me.

Copyright © 2026 Brandon Ruffin. **All rights reserved** — see `NOTICE.md`. No open-source license yet — I'd rather see how this holds up with real drivers before deciding how it should be reused. Publishing publicly on GitHub does allow other GitHub users to view and fork the repository; that's a condition of the platform, not a broader grant.

Want to use this somewhere, or build on it? Open a Discussion and ask. The answer will probably be yes.

---

*Built with AI assistance, from my own trip data and my own operating rules. I'm the driver and the operator, not the developer — and I'd rather say that plainly than pretend otherwise.*
