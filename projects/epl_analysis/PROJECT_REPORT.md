# English Premier League data analysis

## What I found

My original GitHub repository includes the notebooks and two datasets used for the team and match-level exploration:

- [The_best_teams_of_EPL.ipynb](https://github.com/mayurshimbre123/mayurshimbre/blob/master/The_best_teams_of_EPL.ipynb)
- [the_best_teams_of_EPL.ipynb](https://github.com/mayurshimbre123/mayurshimbre/blob/master/the_best_teams_of_EPL.ipynb)
- [results.csv](https://github.com/mayurshimbre123/mayurshimbre/blob/master/results.csv): match results, with columns including `home_team`, `away_team`, goals and season.
- [stats (1).csv](https://github.com/mayurshimbre123/mayurshimbre/blob/master/stats%20(1).csv): team-season totals including wins, losses, goals, shots, passes, cards and other metrics.

Both original notebook variants and the two CSV files are included. Their upstream provenance and redistribution terms are not yet established. Historical outputs are not a fresh reproduction.

## Questions I'd ask now

Which teams have the most wins across seasons? Does the result depend on averaging per season versus totaling across seasons? Are top teams the same when ranked by goals, win percentage or other normalized statistics? Is missingness changing from one season to another?

## How I'd make the analysis reproducible

1. Use the original CSV files in this project’s `data/` folder.
2. Open `reviewed/epl_reproducibility.ipynb`; run the schema checks and transparent aggregation.
3. Add charts only after verifying the counts and missing-value patterns; no unsupported rankings are claimed here.

The point of preserving this older work is to show basic Pandas/EDA capability and clarify caveats, not to turn it into a major AI-engineering resume feature.

## Reproduced results check

The reviewed aggregate read 4,560 matches across 12 seasons. It counts wins by adding home wins to away wins for each club; Manchester United leads this count with 290, followed by Chelsea with 276. This is a total across the dataset, so it is affected by the number of seasons each team played. A win percentage or points per match would answer a different question.
