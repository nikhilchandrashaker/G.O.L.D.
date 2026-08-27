# Giants Gold Standard 🥇

**GOLD — Giants Overall Legacy & Dominance**

A franchise-specific measure of player legacy for the San Francisco Giants (1958–2023). GOLD doesn't ask "how good was this player compared to all of MLB?" It asks:

> **How important was this player to the Giants?**

Every component is scored only against other Giants — so the comparison group is always the franchise, never the league.

---

## The formula

```
GOLD = 0.30 × G (Contribution) + 0.30 × O (Production) + 0.20 × L (Longevity) + 0.20 × D (Dominance)
```

Computed separately for hitters and pitchers (batting and pitching stats aren't mashed into one formula), then scaled 0–100.

| Letter | Component | Weight | What it measures |
|---|---|---|---|
| **G** | Contribution | 30% | How much of the franchise's career production this player accounts for, relative to the single biggest contributor in team history |
| **O** | Production | 30% | The quality of the player's production — career OPS+ (hitters) or ERA+ (pitchers), which are already park- and era-adjusted, so a 1962 season is comparable to a 2023 one |
| **L** | Longevity | 20% | Career length with the Giants — games/innings pitched (70%) blended with seasons played (30%) |
| **D** | Dominance | 20% | How exceptional the player's *best* season was, relative to every other season in Giants history |

### Why these weights
- **G + O (60% combined)** keep the score grounded in actual baseball performance, not just tenure.
- **L (20%)** rewards a long Giants career without letting longevity alone carry a score.
- **D (20%)** separates "very good Giant for a long time" from "had a genuinely dominant peak."

Historical importance was deliberately **not** built into the formula as a direct input — that gets subjective fast. Instead, GOLD lets contribution + production + longevity + dominance speak for themselves, and you can separately check afterward whether the top GOLD players line up with who fans and historians already consider the greatest Giants.

---

## Tiers

| Tier | GOLD Score |
|---|---|
| 🥇 Gold Standard | 95–100 |
| 🥈 Elite Gold | 90–94.9 |
| 🥉 Strong Gold | 80–89.9 |
| Silver | 70–79.9 |
| Bronze | below 70 |

---

## Data & qualification

- **Source:** `SFG_batting.csv` and `SFG_pitching.csv` — season-by-season Giants stats, 1958–2023 (66 seasons, 1,052 batters, 493 pitchers before filtering).
- **Aggregation:** counting stats (HR, RBI, IP, SO, etc.) are summed across a player's full Giants career; rate stats (OPS+, ERA+) are playing-time-weighted averages across their seasons with the club.
- **Qualification thresholds** (to keep small-sample noise off the leaderboard):
  - Hitters: 500+ career plate appearances with the Giants
  - Pitchers: 150+ career innings pitched with the Giants
- **Shrinkage correction:** Rate stats are regressed toward league average (100) in proportion to playing time before being scored. Without this, a reliever who threw 18 innings with an outlier 884 ERA+ season was outranking Gaylord Perry and Madison Bumgarner — a good instinct-check that the raw formula needed dampening for small samples.

---

## Files in this project

| File | Description |
|---|---|
| `GiantsGoldStandard.jsx` | Interactive leaderboard artifact — podium for the top 3, searchable/sortable ledger, click any player to see their G/O/L/D breakdown |
| `GOLD_hitters_leaderboard.csv` | Full ranked list of all 196 qualified hitters with career totals, component scores, GOLD score, and tier |
| `GOLD_pitchers_leaderboard.csv` | Full ranked list of all 158 qualified pitchers with career totals, component scores, GOLD score, and tier |
| `README.md` | This file |

### CSV columns

**Hitters:** `Rank, Name, FirstYear, LastYear, Seasons, Games, PA, HR, RBI, Runs, Hits, OPS_plus, G, O, L, D, GOLD, Tier`

**Pitchers:** `Rank, Name, FirstYear, LastYear, Seasons, IP, Wins, Losses, Saves, SO, ERA_plus, G, O, L, D, GOLD, Tier`

---

## Current leaders

**Hitters**
1. 🥇 Barry Bonds — 96.8 (Gold Standard)
2. 🥈 Willie McCovey — 94.1 (Elite Gold)
3. 🥉 Willie Mays — 93.7 (Elite Gold)

**Pitchers**
1. 🥇 Juan Marichal — 96.3 (Gold Standard)
2. 🥈 Gaylord Perry — 73.7 (Silver)
3. 🥉 Madison Bumgarner — 70.0 (Silver)

---

## Known limitations / ideas for v2

- No fielding or baserunning value beyond stolen bases — GOLD currently skews toward hitting/pitching production only.
- Postseason performance isn't included, which likely underrates players like Bumgarner whose legacy leans heavily on October.
- "Contribution" (G) is volume-based relative to the franchise's single biggest contributor — a different but equally defensible design would use percentile rank instead, which would compress the gap between Bonds and everyone else.
- Component weights (30/30/20/20) were chosen for defensibility, not fit to an external "greatest Giants" ranking — that validation step is a natural next analysis.
