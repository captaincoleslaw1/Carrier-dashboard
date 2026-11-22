# Carrier Dashboard

A city carrier dashboard. First module: the color-coded calendar.

## Calendar (v1.3 — Nov 2026 – Dec 2027)
- Tap **Calendar**, pick your color (Black / Yellow / Blue / Green / Brown / Red),
  and you get your schedule from November 2026 through December 2027: your rotating
  days off highlighted in your color, Sundays off for everyone, all postal holidays
  in that span (gray), and paydays ($).
- Your color is remembered on the device — you only pick it once.
- Header cards show your next day off, next long weekend (Fri–Sun), next holiday,
  and total days off in 2027.

## Leave planner (v1.2, cleaned up in v1.3)
- The color picker is just the picker — no explanation text.
- After picking a color, two fillable boxes appear: **AL Balance** and **SL Balance**
  (hours), in a dark bar that sticks to the top of the screen while you scroll.
- Tap a date once: it turns **green = AL**. Tap again: **blue = SL**. Tap a third
  time: cleared. Every marked day subtracts **8 hours** from that balance, shown
  live in the sticky bar (it goes red if you over-plan past zero).
- **Holiday boxes are red.** A leave tap on a holiday overrides the red with the
  AL/SL color. Sundays can't be marked (already off for everyone).
- Balances and marked days are saved on the device (localStorage), per carrier.

## How the rotation was deciphered (2027 printed calendar)
From the LetterCarrierCalendars.com 2027 color-coded days-off calendar, cross-checked
against a published A–F schedule table (Branch 2200 / CSALC) and against a real
Yellow carrier's known days off — 35/35 dates matched for May–Dec 2027, plus all of
Jan–Apr 2027.

| Letter | Color  |
|--------|--------|
| A | Black  |
| B | Yellow |
| C | Blue   |
| D | Green  |
| E | Brown  |
| F | Red    |

Rotation rule (generates the whole year, no hard-coded table):
Sunday off for all. One rotating day off per week, moving one day later each week
(Mon → Tue → Wed → Thu → Fri), then Fri+Sat together (long weekend), then back to
Monday. Generator anchor: Monday, Nov 2, 2026 = Yellow (B) off; it lands Friday, Jan 1,
2027 on Green (D), matching the printed calendar. Daily order cycles
A→B→C→D→E→F, Saturday repeats Friday's group.

Colors differ between branches — the picker also lets a carrier identify their
color from a known day off (week of Nov 2, 2026).

## 2027 postal holidays
Jan 1 New Year's · Jan 18 MLK · Feb 15 Presidents' · May 31 Memorial ·
Jun 19 Juneteenth · Jul 5 Independence Day (observed) · Sep 6 Labor ·
Oct 11 Columbus · Nov 11 Veterans · Nov 25 Thanksgiving · Dec 25 Christmas

Paydays: every other Friday, anchored on Fri Nov 20, 2026 (a confirmed payday),
starting Nov 6, 2026. 2027 has 26 (Jan 15 – Dec 31). A payday that lands on a
postal holiday pays the day before (Fri Jan 1, 2027 -> Thu Dec 31, 2026).

## Roadmap ideas
- 2026 + 2028 years, month view, "best weeks to take leave" by color
- More dashboard modules (Thomas to define)

v1.3: removed the summary card entirely (next day off / next long weekend /
next holiday / leave-days stats and the instruction paragraph under the
balances). The screen is now: sticky AL/SL bar, then the calendar.

v1.4: cleaned up the sticky balance bar (Thomas called v1.2's layout sloppy —
labels and values wrapped unevenly on a phone). New bar: a color chip + Change
color pill on top, then two equal side-by-side panels (AL green meter, SL blue
meter), each with the hours-left big, a thin meter of what's left, and the
balance input underneath. Header slimmed down to match.

v1.5: date numbers a tad bigger for fat fingers (Thomas's words — not too big):
day font 12px -> 14.5px, cell height 22px -> 32px, a little more padding.

v1.6: one short hint line above the first calendar — "Tap once for AL, twice
for SL" (AL in green, SL in blue). Nothing else; Thomas asked for just that line.

v1.7: same as v1.6, plus the version number is back in the header subtitle
("Calendar · v1.7 · Nov 2026 – Dec 2027") — Thomas couldn't tell whether the
update had landed because v1.4 had dropped the version from the page.

v1.8: bug fix — the v1.6 "Tap once for AL, twice for SL" line was in the page
but never un-hidden (a patch missed its target in renderYear), so it never
appeared. Fixed, and this time verified by simulating a page load with a saved
color: hint, balance bar, and calendar all show; picker hides. Lesson recorded:
assert every patch replacement and test the load path, not just the logic.

v1.9: same balance-card overflow fix Thomas found on Time Wiz — on phone-width
screens the right AL/SL panel overflowed the blue card because "Balance + input
+ hrs" was wider than the panel and the panel wouldn't shrink. Grid columns are
now minmax(0,1fr), panels have min-width:0 + overflow hidden, labels ellipsize,
and the balance input flexes instead of sitting at a fixed 72px.

v1.10: holiday colour changed for everyone — red -> deep purple (#7b3294), a
colour no rotation uses, because Red carriers' days off were red like the
holidays and indistinguishable. Brown (E) darkened from golden brown #a67c2e
to deep chocolate #7c4a1e: Thomas (a bit colour-blind) found brown blended
into red; the new brown separates from red by brightness even where the hues
are hard to tell apart.

v1.11: AL/SL marks are no longer colour-only. A marked day now also carries a
small white "AL"/"SL" tag in the corner plus a white inset ring, because the
AL green is Green carriers' NSD colour and the SL blue is Blue carriers' —
changing the mark colours would just move the collision (and green/blue match
the balance meters). A plain NSD has no tag; a leave day always does, whatever
your colour.

v1.12: Reset button added to the left of "Change color" in the sticky bar.
Reset clears all marked AL/SL days but keeps the entered AL/SL balances (and
the picked colour). It asks first ("Clear all your marked AL/SL days? Your
balances stay as entered.") so a stray tap can't wipe a plan; with nothing
marked it's a no-op. Verified: confirm clears marks only, balances and colour
untouched; declining the prompt leaves marks alone.
