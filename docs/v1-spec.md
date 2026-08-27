# SKARN v1 spec

This file is the lock. The later game PR implements this file. This PR does not add `src/`.

SKARN v1 is one outpost: six named people, four visible places, standing jobs that gate rates, two needs that drain on a persisting clock, three player verbs, one named disaster. It is not a slogan, not a mashup of other games, not a machine circuit, not a spectator, and not a rewind.

## 1. Roster (STUB_)

Exactly six humans. Ids are fixed. Display names are `STUB_` until a later pass replaces the strings only.

| id  | name        | start place | start job | start hunger | start sleep |
| --- | ----------- | ----------- | --------- | ------------ | ----------- |
| h1  | STUB_Ada    | stock       | idle      | STUB_HUNGER_START | STUB_SLEEP_START |
| h2  | STUB_Bram   | stock       | idle      | STUB_HUNGER_START | STUB_SLEEP_START |
| h3  | STUB_Cora   | stock       | idle      | STUB_HUNGER_START | STUB_SLEEP_START |
| h4  | STUB_Dov    | stock       | idle      | STUB_HUNGER_START | STUB_SLEEP_START |
| h5  | STUB_Elin   | stock       | idle      | STUB_HUNGER_START | STUB_SLEEP_START |
| h6  | STUB_Finn   | stock       | idle      | STUB_HUNGER_START | STUB_SLEEP_START |

`STUB_HUNGER_START = 80`. `STUB_SLEEP_START = 80`. Both needs are integers `0..100`.

A person record is always:

```
{ id, place, job, hunger, sleep }
```

No seventh person. No unnamed pawn.

## 2. Places

Exactly four places. They are visible labeled sites, not a fortress map, not tiles-as-the-game, not Z-levels, not fluids.

| place | what the player sees |
| ----- | -------------------- |
| stove | one cook site |
| plot  | one grow site |
| cot   | one rest site |
| stock | counted stores, visible pile |

`person.place` is one of `stove | plot | cot | stock`. There is no other place id.

## 3. Stores

Counted integers on the world, shown at `stock`:

```
stores = { grain: STUB_START_GRAIN, meals: STUB_START_MEALS }
```

`STUB_START_GRAIN = 10`. `STUB_START_MEALS = 4`.

No other store keys in v1.

## 4. Jobs and rates

A job is a standing vacancy plus, if staffed, a rate. Unstaffed job rate is `0`. Idle is not a producing job.

| job  | place | staffed rate (per tick) | unstaffed rate |
| ---- | ----- | ----------------------- | -------------- |
| tend | plot  | `stores.grain += STUB_TEND_GRAIN_PER_TICK` | `0` |
| cook | stove | if `stores.grain >= STUB_COOK_GRAIN_COST`: `grain -= STUB_COOK_GRAIN_COST`, `meals += STUB_COOK_MEALS_PER_TICK`; else `0` | `0` |
| rest | cot   | that person: `sleep += STUB_SLEEP_RECOVER_PER_TICK` (clamp 100) | `0` (no sleep recover) |
| idle | stock | none | none |

`STUB_TEND_GRAIN_PER_TICK = 1`.  
`STUB_COOK_GRAIN_COST = 1`.  
`STUB_COOK_MEALS_PER_TICK = 1`.  
`STUB_SLEEP_RECOVER_PER_TICK = 3`.

Staffed means: at least one person has `job` equal to that job **and** `place` equal to that job's place. Rate is applied once per staffed job per tick, not once per extra body. A second person on the same job does not double the rate in v1.

`idle` people stand at `stock`. They gate no rate.

## 5. Player verbs (exactly three)

The player has three verbs. Not `cut`. Not `walk`. Not `feed`. Not `hold`.

| verb | signature | what it mutates | what it must not do |
| ---- | --------- | --------------- | ------------------- |
| intent | `intent <text>` | overseer reads `text`, writes `posts` | must not call `freshWorld`; must not change `tick` or `stores`; must not assign a person |
| assign | `assign <id> <job>` | one named person: `job`, and `place` = that job's place | must not call `freshWorld`; must not change `tick` or `stores`; rate change happens on the **next** tick |
| veto | `veto <postId>` | removes that row from `posts` | must not call `freshWorld`; must not change `tick` or `stores`; must not move a person |

`id` is one of `h1..h6`. `job` is one of `tend | cook | rest | idle`.

`walk` is internal only: when `assign` sets a job, the person's `place` becomes the job's place in the same call. `walk` is not a player verb. `walk` must not call `freshWorld` and must not rewind `tick` or `stores`.

Clock UI (`pause` / `1x` / `3x`) is not a fourth verb. It only writes `speed`.

## 6. Overseer (rules table, no model key)

The overseer is a static table. No API key. No model call. No LLM-per-person.

`intent <text>` lowercases `text` and applies every matching row. Each match **posts** a standing job if that job is not already posted. It does not assign people.

| rule id | if `text` contains any of | post |
| ------- | ------------------------- | ---- |
| r1 | `survive`, `fed`, `food`, `hunger`, `larder` | `{ id: p_tend, job: tend, place: plot, source: r1 }` and `{ id: p_cook, job: cook, place: stove, source: r1 }` |
| r2 | `sleep`, `rest`, `tired` | `{ id: p_rest, job: rest, place: cot, source: r2 }` |
| r3 | no row matches | post nothing; `posts` unchanged |

Post ids are stable: `p_tend`, `p_cook`, `p_rest`. A post is a vacancy the player can fill with `assign`. People do not auto-take posts in v1.

`veto p_cook` removes `p_cook`. It does not idle a cook already assigned.

## 7. One named order changes a job and a rate on the next tick

Concrete sequence (this is the lock, not an example slogan):

1. World at `tick = N`, `h2.job = idle`, `h2.place = stock`, no one has `job = tend`, so tend rate is `0`. `stores.grain = G`.
2. Player: `assign h2 tend`.
3. Same call, still `tick = N`, still `stores.grain = G`. Now `h2.job = tend`, `h2.place = plot`.
4. Next `applyTick`: `tick = N+1`, tend is staffed, `stores.grain = G + STUB_TEND_GRAIN_PER_TICK`.

If step 2 is skipped, tend stays unstaffed and grain does not move from tend.

## 8. Clock

`tick` is an integer. It starts at `0`. It only increases inside `applyTick`. It persists for the life of the world.

`speed` is one of `pause | 1x | 3x`.

| speed | wall clock | ticks applied |
| ----- | ---------- | ------------- |
| pause | running | `0` |
| 1x | every `STUB_TICK_MS` | `applyTick()` once |
| 3x | every `STUB_TICK_MS` | `applyTick()` three times |

`STUB_TICK_MS = 1000`.

`intent`, `assign`, `veto`, and internal `walk` **must not**:

- call `freshWorld`
- set `tick` to a smaller value
- restore `stores` to an older snapshot
- rebuild the roster

There is no rewind.

## 9. Needs (hunger, sleep)

Both drain on the clock, every `applyTick`, after `tick += 1`, before job rates.

| need | drain per tick | recover |
| ---- | -------------- | ------- |
| hunger | `hunger -= STUB_HUNGER_DRAIN_PER_TICK` (clamp 0) | if `stores.meals >= 1` and `hunger <= STUB_EAT_THRESHOLD`: `meals -= 1`, `hunger += STUB_MEAL_HUNGER` (clamp 100). At most one meal per person per tick. |
| sleep | `sleep -= STUB_SLEEP_DRAIN_PER_TICK` (clamp 0) unless `job === rest` | `rest` as in §4 |

`STUB_HUNGER_DRAIN_PER_TICK = 1`.  
`STUB_SLEEP_DRAIN_PER_TICK = 1`.  
`STUB_EAT_THRESHOLD = 50`.  
`STUB_MEAL_HUNGER = 20`.

Needs do not create a third store. They live on the person.

## 10. Speed controls

Visible controls write `speed` only: `pause`, `1x`, `3x`. They do not call `freshWorld`. They do not change `stores`, people, or `posts`. `pause` is a stop (see §12).

## 11. One named watchable disaster: `larder_empty`

There is one disaster id: `larder_empty`. The player can see it on the dump at all times (`none` or `larder_empty`).

Trigger (STUB_ until measured in play):

```
disaster becomes larder_empty when
  stores.grain === 0
  AND stores.meals === 0
  AND some person has hunger === 0
```

`STUB_` on this trigger means the thresholds are the v1 lock even if later balance changes the numbers, not the name.

When it fires: `disaster = "larder_empty"`, `speed = "pause"`. The dump still shows people, stores, tick, and posts. The world does not rewind.

## 12. Stop

The world stops applying ticks when:

- `speed === "pause"`, or
- `disaster === "larder_empty"` (which forces pause)

Stop is not cut-until-HOLD. There is no `cut` verb and no HOLD state.

## 13. Tick order (`applyTick`)

If `speed === "pause"` or `disaster !== "none"`: return.

1. `tick += 1`
2. every person: drain hunger and sleep (§9)
3. every person with `hunger <= STUB_EAT_THRESHOLD`: try one meal (§9)
4. apply staffed job rates once each (§4)
5. evaluate `larder_empty` (§11)

## 14. Dump shape

`dump()` returns exactly this shape. No extra top-level keys in v1.

```json
{
  "tick": 0,
  "stores": { "grain": 10, "meals": 4 },
  "people": [
    { "id": "h1", "place": "stock", "job": "idle", "hunger": 80, "sleep": 80 },
    { "id": "h2", "place": "stock", "job": "idle", "hunger": 80, "sleep": 80 },
    { "id": "h3", "place": "stock", "job": "idle", "hunger": 80, "sleep": 80 },
    { "id": "h4", "place": "stock", "job": "idle", "hunger": 80, "sleep": 80 },
    { "id": "h5", "place": "stock", "job": "idle", "hunger": 80, "sleep": 80 },
    { "id": "h6", "place": "stock", "job": "idle", "hunger": 80, "sleep": 80 }
  ],
  "posts": [],
  "speed": "pause",
  "disaster": "none"
}
```

`posts` item: `{ "id": "p_tend"|"p_cook"|"p_rest", "job": "tend"|"cook"|"rest", "place": "plot"|"stove"|"cot", "source": "r1"|"r2" }`.

`disaster` is `"none"` or `"larder_empty"`.

## 15. Done-when (later game PR, not this PR)

The game PR is done when a human or test can do this in one run, without `freshWorld`:

1. `intent survive` — `posts` contains `p_tend` and `p_cook`.
2. `assign h2 tend` — `people[h2].job === "tend"`, `people[h2].place === "plot"`.
3. `speed = 1x` long enough for one `applyTick` — `tick` is larger than before the assign; `tick` is not smaller.
4. `stores.grain` is larger than it was at assign time by `STUB_TEND_GRAIN_PER_TICK` (rate moved because the job was staffed).
5. `dump().disaster` is readable (`none` or `larder_empty`). The field is visible even if it has not fired.

If assign is omitted, tend rate stays `0` and grain does not gain the tend increment.

## 16. Out (v1 must not contain)

orbit, Jita, paldex, PoE, KSP, cooler, dwarves, Godot, tiles-as-the-game, 200 items, LLM-per-person, cut-as-the-verb, rewind.

Also out: fortress map, Z, fluids, spectator (player never orders), machine circuit, `freshWorld` on intent/assign/veto/walk, cut-until-HOLD.

## 17. This PR

Adds `docs/v1-spec.md` only (plus a README pointer). No game source. Scaffold and sim come after this lock.
