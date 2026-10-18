# RimRunnerAlaska

Unofficial Alaska HS boys basketball ratings. Not affiliated with the ASAA or MaxPreps.
Status: **HELD (waiting on hosting)**. Preview: https://joshua-kpg.github.io/RimRunnerAlaska/ (GitHub Pages). No Firebase project yet
(the Google accounts are at their project quota) and Cloudflare Pages is at its project limit, so accounts, picks and follows save only in the
visitor's browser until the site's own Firebase project exists.

## Files
- `index.html` — the whole app (data embedded). `logos/` — small WebP school logos (from MaxPreps school profiles), served with the site.
- `data/results.json` — 2026-27 finals ledger written by the nightly updater.
- `firebase/` — Firestore rules and auth config for the site's future Firebase project (accounts, picks, follows).

## Teams
141 teams: the ASAA 2026-27 boys basketball teams (ASAA 2026-27 Handbook, "Basketball Conferences") that have a MaxPreps varsity team with games:
4A 20, 3A 16, 2A 21, 1A 84. Conferences = the 22 ASAA basketball conferences (4A Cook Inlet, Mid Alaska, Northern Lights, Southeast; 3A Aurora,
Southcentral, Southeast, Western; 2A Interior, Northwest, Southeast, Southern; 1A Alaska Coastal, Aleutian Chain, Bering Sea, Golden Heart,
Greater Kuskokwim, North Slope, Northwest Arctic, Peninsula, Southeast, Yukon Delta). No Other (non-ASAA) programs met the 8-game rule.

## Season rule
ASAA 2026-27 boys basketball First Contest = Thu Dec 17, 2026 (all classes; first practice Dec 2). Games involving an ASAA school before that
date are left out (schedule build and nightly updater); games between two non-ASAA schools are kept. State: 1A Mar 10-13, 2A Mar 11-13,
3A/4A Mar 17-20, 2027 (Alaska Airlines Center, Anchorage).

## Nightly scores
`.github/workflows/nightly-scores.yml` runs `scripts/update_scores.py` at 08:30 and 16:00 UTC (11:30 pm / 7:00 am Alaska standard time) and
on manual dispatch. Before `SEASON_START` in index.html (the first game on the MaxPreps schedules) the script makes no requests. From then on it
reads boys basketball finals for the last 3 days from the MaxPreps Alaska scores-by-date page (team-page fallback), matches them to the schedule
by MaxPreps team id + date, records them in `data/results.json` and bakes scores and W-L records into `index.html`. The page recomputes Elo
from those finals. It commits only when data changed; GitHub Pages updates from the commit.
