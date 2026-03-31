# Verification Loop

Verification strategy for unresolved findings after intake.

## Signals

- Strong: confirmed fact, write/update immediately
- Moderate: write with `(unverified)`, then verify
- Speculative: queue only, do not write as fact

## Queue File

`Verification_Queue.md` columns:
- `lead_id`
- `person`
- `signal` (`moderate`, `speculative`)
- `evidence`
- `attempts`
- `next_step`
- `status` (`open`, `escalated`, `cold`, `resolved`)

## Moderate Loop

- maximum 2 attempts
- if corroboration found -> `resolved`
- if unresolved -> keep `escalated` for future evidence

## Speculative Loop

- maximum 3 attempts
- if corroboration found -> promote and `resolved`
- if unresolved after attempt 3 -> `cold`

## Status Transitions

- `open -> resolved`
- `open -> escalated`
- `open -> cold` (speculative exhausted)
- `escalated -> resolved`

## Runtime Interaction

After verification pass:
- update `Runtime_State.md` phase to `verify_done`
- if external evidence is required, set `waiting_for_manual_batch`
- append checkpoint summary to `Research_Log.md`

## Safety

- No unbounded retries
- No confirmation without corroboration
- No overwrite of stronger confidence data
