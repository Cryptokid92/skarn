# SKARN Harper v1 brief

Date: 27 Aug 2026. Repo: https://github.com/Cryptokid92/skarn @ `09bce69923c80459758b9e6ec11d348b058c3680`. Docs only. No game `src`. No No Part or Stonewatch code.

Access dates below are 27 Aug 2026 unless a page states an earlier last-edit.

---

## Asked

v1 rates and comparables for **standing work** + **needs / designate**.

Steal **only**:

- RimWorld **Work** (standing assignments) + **Bills** (target / forever / count).
- Dwarf Fortress **Manager** work orders + **needs** (hunger / sleep that interrupt labor) and **designate** (mark a place for work).

State what SKARN **must not clone** from Stonewatch or No Part.

Numeric hunger / sleep / job rates: cite an order of magnitude from a source, or mark `STUB_`. Do not invent a number and call it nature.

---

## Known

### SKARN lock (this repo)

- SKARN is a living outpost. New repo. All new code. Not No Part. Not Stonewatch. Source: `README.md` @ `09bce69`, 27 Aug 2026.
- Player is principal. Type intent. Overseer (rules, no key) posts standing jobs. Named people take them. Needs drain. Clock does not rewind. Watch, pause, assign, veto. Do not cut machines until HOLD. Source: same `README.md`.
- **v1 in:** RimWorld standing work + DF needs/designate only; six named humans; visible places stove, plot, cot, stock; hunger and sleep; jobs that gate a rate; unstaffed = 0; pause / 1x / 3x; one watchable disaster; Vite + TypeScript browser. Source: same `README.md`.
- **v1 out:** Orbit, Jita, paldex, PoE tree, KSP editor, cooler, dwarves, Godot, tiles-as-the-game, 200 items, LLM-per-person, cut-as-the-verb, `freshWorld` rewind. Source: same `README.md`.
- Later modules stay on this kernel: jobs as physics, one industry chain, counted stock, one labor creature, one site vehicle, one launch, one price. Source: same `README.md`.
- Repo has no `evidence/` tree and no product `src`. This brief lives at `docs/brief.md`. Source: tree of `Cryptokid92/skarn` @ `09bce69`, 27 Aug 2026.

### RimWorld — standing work and bills (steal shape only)

- Work is a standing assignment grid: which colonist may do which work type. Default mode is checkbox-on/off. Manual priorities use 1–4 (1 highest). Equal numbers break left-to-right on the Work tab. Source: RimWorld Wiki [Work](https://rimworldwiki.com/wiki/Work), retrieved 27 Aug 2026; also [Colonist](https://mail.rimworldwiki.com/wiki/Colonist), retrieved 27 Aug 2026.
- A pawn can be right-clicked onto a target (blueprint, object, pawn) for one immediate job, only if assigned that work type. Shift queues. Source: RimWorld Wiki [Work](https://rimworldwiki.com/wiki/Work), retrieved 27 Aug 2026.
- Bills sit on production buildings. Assigned pawns attempt bills. Modes: **Do X times**, **Do until you have X**, **Do forever**. Source: RimWorld Wiki [Bill](https://www.rimworldwiki.com/wiki/Bill), retrieved 27 Aug 2026 (search-index text; live wiki was Cloudflare-gated this session).
- **Do until you have X** can **Pause when satisfied** and **Unpause at: x**. Items not in a stockpile are not counted. Unpause threshold is kept below the target count. Source: same Bill page; also RimWorld English keyed strings `PauseWhenSatisfied` / `UnpauseWhenYouHave` in [RimWorld-zh/RimWorld-English `Dialogs_Various.xml`](https://github.com/RimWorld-zh/RimWorld-English/blob/master/Keyed/Dialogs_Various.xml), retrieved 27 Aug 2026.
- **Do forever** stops only when materials run out. Source: RimWorld Wiki [Bill](https://www.rimworldwiki.com/wiki/Bill), retrieved 27 Aug 2026.
- Schedule **Anything**: work until food need < 30%, rest need < 30%, or recreation < 35%, then fulfill the need. Schedule **Work**: eat at food < 30%; ignore sleep/recreation until rest hits 0 and the pawn collapses, then wakes at 20% rest. Schedule **Sleep**: seek rest at rest < 75%. Source: RimWorld Wiki [Schedule](https://rimworldwiki.com/wiki/Schedule) / [Menus](https://www.rimworldwiki.com/wiki/Menus), retrieved 27 Aug 2026.

### RimWorld — hunger / sleep rates (order of magnitude)

- Adult baseline human hunger rate: **1.6 nutrition per day**. Max stored nutrition: **1.0**. Hungry band starts at **0.25** saturation. Pawns try to eat at **~30%** saturation. Source: RimWorld Wiki [Food](https://rimworldwiki.com/wiki/Food) and [Saturation](https://www.rimworldwiki.com/wiki/Saturation#General_mechanics), retrieved 27 Aug 2026.
- Simple meal: **0.9** nutrition eaten, **0.5** raw nutrition to cook. Rough colony planning figure: **~2 simple meals per adult per day** (1.6 / 0.9 ≈ 1.8). Source: RimWorld Wiki [Food](https://rimworldwiki.com/wiki/Food) and [Simple meal](https://rimworldwiki.com/wiki/Simple_meal), retrieved 27 Aug 2026.
- Simple meal work to make: **300 ticks (5 seconds at 1×)**. Campfire doubles to **600 ticks**. A RimWorld game day is **60,000 ticks**, so 300 ticks is **0.5% of a game day** (~7 game-minutes) of bench time per meal, before Cooking Speed. Source: RimWorld Wiki [Simple meal](https://rimworldwiki.com/wiki/Simple_meal) and [Rest](https://www.rimworldwiki.com/wiki/Rest) (ticks-per-day), retrieved 27 Aug 2026.
- Rest while awake falls in pieces. From 100% rest, **Drowsy** (~28%) in **~18.2 game hours**; **Tired** (~14%) after **~23.2 game hours**; **Exhausted** (~1%) after **~34.2 game hours**. Collapse / sleep-on-spot at **0%**. Source: RimWorld Wiki [Rest](https://www.rimworldwiki.com/wiki/Rest), retrieved 27 Aug 2026.
- Sleep recover 0% → 100% at 100% Rest Effectiveness and 100% Rest Rate Multiplier: **10.5 game hours (26,250 ticks)**. From the Tired band (~28%) in a normal bed: **~7.56 game hours**. Ground / sleeping spot is 0.8× that recover rate. Source: same Rest page.
- Balance point on an unmodified pawn in a normal bed, staying out of Drowsy: **~17 game hours awake / ~7 game hours asleep per 24h**. Source: same Rest page (solved from the published 0.95/day awake fall vs 24/10.5 recover).

### Dwarf Fortress — manager, work orders, designate (steal shape only)

- Designations **mark tiles** for a labor: mine, channel, stairs, chop, gather, smooth, engrave, dump/forbid, traffic, and remove-designation. Paint rectangle or per-tile. Priority **1 (highest) through 7 (lowest)**; default 4. **Blueprint** marks without starting the job; a later toggle makes them live. A dwarf picks the nearest eligible designated tile (max-norm distance), not the globally “best” job. Source: DF Wiki [Designations menu](https://dwarffortresswiki.org/index.php/Designations), last edited 25 May 2026, retrieved 27 Aug 2026.
- A **Manager** noble + meager office unlocks fortress-wide **work orders**: queue production from one screen instead of clicking each workshop. After **20 citizens**, orders wait for manager validation in the office. Source: DF Wiki [Manager](https://dwarffortresswiki.org/index.php/Manager), retrieved 27 Aug 2026.
- Work orders repeat on a clock: one-time, or restart if completed, conditions checked **daily / monthly / seasonally / yearly**. Multiple conditions are **AND**. Item conditions are amount + equality + type/material/adjective (keep-X / at-most-X). Orders may depend on another order starting or finishing. Workshop-local orders exist; a shop can set “general work orders allowed” to 0. Source: DF Wiki [Work orders](https://dwarffortresswiki.org/index.php/Work_order), retrieved 27 Aug 2026.
- Labor model: jobs are created by designations, zones, workshop tasks, and manager orders. An idle dwarf with the labor enabled takes the job. Eating, sleeping, and drinking appear as jobs but are **not assigned**; they are created when the counters demand them. Source: DF Wiki [DF2014:Labor](https://dwarffortresswiki.org/index.php/DF2014:Labor), retrieved 27 Aug 2026.
- Fortress time: **1,200 ticks / day**, 33,600 / month, 100,800 / season, 403,200 / year. Source: DF Wiki [Time](https://dwarffortresswiki.org/index.php/Time), retrieved 27 Aug 2026.

### Dwarf Fortress — hunger / sleep / “Need” (two different systems)

- **Hunger (biological):** counter **+1 per tick** (doubled if a mother is carrying a child). Idle consider-eat **40,000**; idle will-eat **45,000**; flash Hungry **50,000**; unhappy + cancel job **65,000**; flash Starving + vermin **75,000**; fat burn starts **100,000**, then death when fat is gone. An Eat job **−50,000** (floor 0). Planning rule of thumb: **~2 food units per dwarf per season**. Source: DF Wiki [Food](https://dwarffortresswiki.org/index.php/Food) (redirect from Hunger), retrieved 27 Aug 2026.
- Order of magnitude from those ticks: Hungry flash at 50,000 / 1,200 ≈ **42 days**; Starving flash ≈ **62 days**; fat-burn start ≈ **83 days**. Eat −50,000 vs +403,200 / year ⇒ **~8 eat jobs / year ≈ 2 / season**. Source: same Food page + [Time](https://dwarffortresswiki.org/index.php/Time), retrieved 27 Aug 2026.
- **Drowsiness (biological):** **+1 per tick** awake. Idle consider-sleep **50,000**; idle will-sleep **54,000**; flash Drowsy **57,600**; Tired thought **65,000**; Very Drowsy **150,000**; Exhausted thought **160,000**; **insane at 200,000**. Sleep **−19 per tick** to 0; typical sleep **2,650–2,900 ticks (~2.2–2.4 days)**. Wiki states dwarves spend **exactly 5%** of life sleeping. Unable to sleep **~6 months** may go insane (200,000 / 1,200 ≈ 167 days). Source: DF Wiki [Sleep](https://dwarffortresswiki.org/index.php/Sleep), last edited 2 Apr 2025, retrieved 27 Aug 2026.
- **Need (psychological / focus):** a separate system. Unmet needs damage **focus** (skill quality), not a hunger bar. Satisfying a need refreshes it to 400. High-priority personal jobs (magenta) will not yield to fortress work; low-priority (green) may. Rule of thumb to keep a need out of “Distracted”: fulfill every **2 years / 1 year / 6 months / 3 months** at need weights 1 / 2 / 5 / 10 (alcohol excepted). Source: DF Wiki [Need](https://dwarffortresswiki.org/index.php/Need), retrieved 27 Aug 2026 (page notes possible v47→v53 drift).
- SKARN v1 lock is **hunger and sleep**, not the DF focus catalog. Steal the **interrupt** (needs create jobs that beat standing work), not 20+ personality needs. Source: SKARN `README.md` @ `09bce69` vs DF Wiki [Need](https://dwarffortresswiki.org/index.php/Need), both retrieved 27 Aug 2026.

### Real-world order of magnitude (not a SKARN rate)

- Adults: **7 or more hours** sleep per night. Source: Watson et al., AASM/SRS consensus, *Sleep* 2015; 38(6):843–844, https://doi.org/10.5665/sleep.4716 ; CDC [About Sleep](https://www.cdc.gov/sleep/about/index.html) citing that statement, retrieved 27 Aug 2026.
- Survival without food, with water: commonly reported **weeks, often cited 1–2 months**, highly individual. **Not** a precise constant. Source: Medical News Today, “How long can you go without food?”, retrieved 27 Aug 2026, https://www.medicalnewstoday.com/articles/how-long-can-you-go-without-food

### Stonewatch — what it is (do not clone)

- Spectator fortress. **Player never gives orders.** Godot 4 desktop, GDScript, 2D pixel tiles. World 64×64 **and** one live 160×160 hall, both on screen. 15 dwarves embark, cap 40. No Z, no fluids. Drama director steals the camera and writes a chronicle. Overseer auto-posts a carve sequence. Hall death → ruin → automatic re-embark. Speeds include **10×**. Source: `Cryptokid92/Stonewatch` `docs/product-spec.md` and `README.md`, product lock 23 Aug 2026, retrieved 27 Aug 2026.
- CoS assumptions (23 Aug 2026): starve visible in a short demo; tantrum then raid; fortress tick vs world month-per-fortress-week; no save in v1; no LLM dwarves. Source: Stonewatch `docs/cos-brief.md` and `docs/decision-log.md`, 23 Aug 2026.

### No Part — what it is (do not clone)

- Private sibling. README lock: v1 `gen` and `kitchen`, one circuit, no cooler; leftover food leaks power **1:1**; `feed` is the food need; v2 planner + named crew, **jobs are labels**, kernel unchanged; v3 `walk <id> gen|kitchen`, **presence is the job**, unstaffed living parts apply rate 0. Source: `Cryptokid92/no-part` `README.md`, retrieved 27 Aug 2026.
- Filename surface only (not copied): `src/commands.ts`, `game.ts`, `overseer.ts`, `parts.ts`, `planner.ts`, `sim.ts`, `stubs.ts`, plus tests and HTML. Source: listing of `Cryptokid92/no-part` `src/`, 27 Aug 2026.
- Evidence rule there: Grok Build writes only under `evidence/<name>/`; nobody writes `src/`, tests, CI, or HTML from an evidence log. Source: `no-part` `evidence/README.md`, retrieved 27 Aug 2026. SKARN has no `evidence/` tree; this brief does not copy that layout or that kernel.

### Comparables table (sourced OOM or STUB_)

| Quantity | SKARN v1 | Comparable OOM | Source / date |
|---|---|---|---|
| Hunger drain | `STUB_` | RW **1.6 nutrition / day**; eat seek ~**30%** bar | RW Food / Saturation, retrieved 27 Aug 2026 |
| Hunger meal size | `STUB_` | RW simple meal **0.9** nutrition; ~**2 meals / adult / day** | RW Food / Simple meal, retrieved 27 Aug 2026 |
| Hunger to starve | `STUB_` | RW malnutrition at **0** sat after ~**1 game day** unfed from empty; DF Hungry flash **~40 days**, fat-burn **~80 days** | RW Saturation; DF Food + Time, retrieved 27 Aug 2026 |
| Sleep drain (awake) | `STUB_` | RW **~18 h** to Drowsy from full; collapse **~1–1.5 game days**. DF drowsy flash **~48 days**; insane if unslept **~6 months** | RW Rest; DF Sleep, retrieved 27 Aug 2026 |
| Sleep recover | `STUB_` | Real **≥7 h / night**. RW **~7–10.5 game hours** in bed. DF sleep bout **~2 days**, **5%** of life | AASM 2015; RW Rest; DF Sleep |
| Stove / cook job | `STUB_` | RW simple meal **300 ticks ≈ 0.5% of a RW day** of bench time | RW Simple meal + Rest ticks/day, retrieved 27 Aug 2026 |
| Plot / grow job | `STUB_` | DF default crop `GROWDUR` **300 ≡ 30,000 ticks ≈ 25 fortress days** (wiki default; not a SKARN number) | DF Time (GROWDUR), retrieved 27 Aug 2026 |
| Staffed job rate | `STUB_` | SKARN lock: **unstaffed = 0**. Staffed magnitude is not in this repo | SKARN `README.md` @ `09bce69` |
| Standing work | steal RW Work + Bills | Priorities + Do-until-X / forever | RW Work / Bill, retrieved 27 Aug 2026 |
| Designate | steal DF mark-a-place | Priority + live vs blueprint; **not** a tile world as the game | DF Designations, 25 May 2026; SKARN v1-out tiles-as-the-game |
| Manager keep-X | steal DF work orders | Amount/equality conditions; daily..yearly restart | DF Work orders / Manager, retrieved 27 Aug 2026 |
| Need interrupt | steal DF + RW | Hunger/sleep create a job that beats standing work | DF Labor / Food / Sleep; RW Schedule |

---

## Contested

- **Which clock SKARN hunger uses.** RW hunger is a **daily** bar. DF biological hunger is a **seasonal** bar (~2 meals / season). Copying both numbers is incoherent. SKARN README does not pick a day length. A 3× watchable starve on a DF-season clock is a long sit; on a RW-day clock it is a short sit. Stonewatch CoS assumed “starve visible in a short demo” (23 Aug 2026) — that is **their** demo constraint, not a SKARN number.
- **Whether “designate” implies a tile map.** DF designations paint tiles. SKARN v1-out is **tiles-as-the-game**. The steal is “mark a place for work” on the four named places (stove, plot, cot, stock), not a 160×160 dig.
- **Whether the Overseer auto-runs a carve script.** Stonewatch overseer posts a fixed hall sequence and the player never orders. SKARN overseer “posts standing jobs” and the player **assign / veto**. Same English word, opposite agency.
- **Unstaffed = 0 vs No Part v3.** SKARN README already locks “jobs that gate a rate; unstaffed = 0”. No Part v3 implemented that as `walk <id> gen\|kitchen` (presence is the job). The **rule** is in-scope. The **walk/presence/gen/kitchen kernel** is not.
- **DF Need (focus) vs hunger/sleep.** “DF needs” in the ask can mean the focus catalog or the biological counters. v1-in names only hunger and sleep. Importing prayer / alcohol / romance focus is out of v1 unless Nikolai widens the lock.
- **Bill on stove vs bill on plot.** RW bills live on benches. DF farm plots are a different UI (grow lists), not manager work orders. Whether plot is a keep-X bill or a designate is unset.
- **One watchable disaster.** Stonewatch’s chain is starve / tantrum / raid plus ruin/re-embark. SKARN v1-out includes dwarves, Godot, tiles-as-the-game, and rewind. Disaster identity is unset; cloning the Stonewatch chain is not the steal.
- **Job as continuous rate vs discrete task.** RW bills and DF orders create **tasks**. SKARN README says jobs **gate a rate**. Those are compatible (task in progress ⇒ rate, else 0) but not the same code shape as No Part’s living-part leak.

---

## Unknown

- SKARN hunger drain, meal size, starve threshold: `STUB_`.
- SKARN sleep drain, cot recover, collapse threshold: `STUB_`.
- SKARN staffed stove / plot / stock rates: `STUB_`.
- How designate works with four named places and no tile map.
- Whether bills attach only to stove, or also to plot / stock.
- The six names, starting stock, starting need values.
- Disaster identity and whether it is hunger-collapse, unstaffed-stove, or something else.
- Tick: wall-clock vs named sim-day; what 1× means in minutes of hunger.
- Whether people path between places or are simply assigned (presence).
- Whether Overseer is a pure rule table (README: “rules, no key”) or a planner.
- Whether keep-X counts **stock** only, or also in-progress meals (RW: stockpile-only).

---

## Must not clone

Mechanics to steal are listed above. Everything else from the two siblings is out, including code.

### From Stonewatch

- Spectator contract (player never gives orders).
- Godot 4, GDScript, scene-tree-as-sim, 2D tiles as the game.
- Dwarves, 160×160 hall, 15/40 pop, dual world+fortress view.
- Drama director, chronicle, camera steal, idle-timeout snap-back.
- Auto hall-carve overseer; automatic ruin → re-embark.
- World clock coupled to fortress week; armies-as-dots.
- 10× speed (SKARN v1 is pause / 1× / 3× only).
- A* on a tile grid as the play.
- Tantrum / raid / magma-adjacent combat kit.
- LLM dwarves, Z-levels, fluids, 200 item types.
- Any file under Stonewatch `sim/`, `view/`, `world/`, `director/`.

### From No Part

- `gen` / `kitchen` one-circuit kernel.
- Leftover food leaks power 1:1.
- `feed` as the need name / physics.
- Jobs as labels (v2).
- `walk <id> gen|kitchen` and “presence is the job” **implementation**.
- Cooler (also SKARN v1-out).
- Cut as the verb; The Cut typing `src/`.
- Planner / command language / `freshWorld` rewind.
- Copy or mechanical edit of `src/game.ts`, `sim.ts`, `parts.ts`, `commands.ts`, `overseer.ts`, `planner.ts`, or tests/HTML.
- LLM-per-person (also SKARN v1-out).

### Also out (SKARN README)

Orbit, Jita, paldex, PoE tree, KSP editor, 200 items.

---

## What would change it

- **Nikolai lock** on hunger / sleep / job numbers, or a signed v1 spec that picks RW-day vs DF-season.
- **Play at 1× and 3×:** if a six-person stove/plot loop cannot show hunger move in one sitting, the clock (not “nature”) must be named and stubbed.
- **Wiki correction:** RW Saturation / Rest tables or DF Food / Sleep thresholds edited after 27 Aug 2026.
- **Decision: designate-without-tiles** — if places are only four nouns, DF paint-rectangle drops out; only priority + live/blueprint + keep-X remain.
- **Decision: need catalog** — if v1 stays hunger+sleep, DF focus weights stay out.
- **Decision: disaster** — picking starve-in-demo vs unstaffed-rate-0 vs something else sets whether hunger OOM must be demo-short (hours of 1×) or sim-long (days).
- **Sibling spec agent** publishing `docs/spec.md` (or similar) that contradicts this brief: the spec lock wins; this file records sources, not law.

`STUB_` rows stay stub until one of the above fires. Do not fill them from taste.
