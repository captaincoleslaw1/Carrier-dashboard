# Carrier Dashboard

A city carrier dashboard. First module: the color-coded calendar.

## Calendar (v1.2 — Nov 2026 – Dec 2027)
- Tap **Calendar**, pick your color (Black / Yellow / Blue / Green / Brown / Red),
  and you get your schedule from November 2026 through December 2027: your rotating
  days off highlighted in your color, Sundays off for everyone, all postal holidays
  in that span (gray), and paydays ($).
- Your color is remembered on the device — you only pick it once.
- Header cards show your next day off, next long weekend (Fri–Sun), next holiday,
  and total days off in 2027.

## Leave planner (v1.2)
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
