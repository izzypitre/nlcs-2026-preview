# Brewers vs. Dodgers: 2026 NLCS Preview

A data-driven preview of the 2026 NLCS between the Milwaukee Brewers and Los Angeles Dodgers, built in Python. The project compares both teams' 2025 and 2026 regular seasons and uses a simple simulation model to estimate each team's chances of winning the series.

**The question:** Third time's a charm for the Brewers, or a third straight World Series trip for the Dodgers? The Dodgers beat Milwaukee in the 2018 NLCS (Game 7) and swept them in the 2025 NLCS. Is this year different?

## Key findings

| | Brewers | Dodgers |
|---|---|---|
| 2026 record | 103-59 (best in MLB) | 100-62 |
| Run differential (2025 → 2026) | +172 → +214 | +142 → +201 |
| Runs scored per game (2025 → 2026) | 4.98 → 5.14 | 5.09 → 4.94 |
| Runs allowed per game (2025 → 2026) | 3.91 → 3.81 | 4.22 → 3.70 |

1. **Both teams are better than last October.** Each improved its run differential by 40+ runs.
2. **They improved in opposite ways.** The Brewers became the better offense; the Dodgers made a big jump in run prevention while their offense slipped.
3. **The regular season series may not tell us much.** The Brewers won the 2026 season series 4-3 but were outscored 27-25, largely due to one 11-3 loss. In 2025 they won all six regular-season meetings, then were swept in the NLCS.

![How each team changed from 2025 to 2026](brewers_dodgers_2025_vs_2026.png)

## Prediction model

A simple, explainable baseline model:

1. **Pythagorean expectation** estimates each team's "true" winning percentage from runs scored and allowed (exponent 1.83).
2. **Log5** converts the two teams' strengths into a single-game win probability.
3. A **home-field adjustment** of 4 percentage points is applied to each game.
4. A **Monte Carlo simulation** plays the series 100,000 times using the real 2-3-2 home schedule (Brewers have home field).

**Result:** a near coin flip. Brewers 51.9%, Dodgers 48.1%, with six- and seven-game series the most likely outcomes. The single most likely result is Brewers in 7.

![Simulated NLCS outcomes](nlcs_series_simulation.png)

## Data and methods

- **Source:** game-by-game results from Baseball Reference via the `pybaseball` Python library.
- **Validation:** season records and run differentials were cross-checked against official MLB.com figures.
- **Data corrections:**
  - The source mixes regular season and postseason games, so analysis uses only the first 162 completed games.
  - The 2025 data was missing each team's final regular-season game (September 28, 2025). Both games were added manually from verified box scores (Brewers 4, Reds 2; Dodgers 6, Mariners 1), and the notebook documents the fix.

## Limitations

- Runs are not adjusted for ballpark effects.
- The model treats every game as having the same odds and does not account for starting pitchers, injuries, or roster changes.
- The model uses regular-season data only and has not been backtested on past postseason series. Backtesting would be the next step to measure its
