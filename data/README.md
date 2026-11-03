# Data sources

This folder holds the data behind "Where did all the goals go?" (Kiven Teoh, FIT3179 Data Visualisation, Monash University, November 2026).
## Sources

| Source | Author | Link | Used for |
|---|---|---|---|
| All games in chronological order, 1897–2026 (17,056 games) | AFL Tables (Paul Jones) | https://afltables.com/afl/stats/biglists/bg3.txt | All scoring, club, margin and venue figures |
| National, state and territory population, March 2026 | Australian Bureau of Statistics | https://www.abs.gov.au/statistics/people/population/national-state-and-territory-population/latest-release | Games per 100,000 residents |
| australian-states GeoJSON | Rowan Hogan | https://github.com/rowanhogan/australian-states | State boundaries on the maps |
| Stadium pages | Wikipedia contributors | Listed per venue in `venue_sources.csv` | Venue coordinates |
| Rule change and playing style articles | AFL, Essendon FC, University of South Australia | Listed in the page footer | Rule dates and tactics |

The AFL Tables file was downloaded by hand. The population figures were copied from the ABS release, and the boundaries were simplified to reduce the file size.

## Files

| File | Where it Comes from | What it holds |
|---|---|---|
| `seasons.csv` | AFL Tables | Games, average total points, goals, behinds and accuracy for each season |
| `team_season.csv` | AFL Tables | Each current club's points per game by season since 1990 |
| `team_rank.csv` | AFL Tables | Each club's scoring rank and points per game by season since 2010 |
| `margin_density.csv` | AFL Tables | Smoothed distribution of winning margins by decade, for the ridgeline chart |
| `close_games.csv` | AFL Tables | Games won by under 6 points, and the median margin, by decade |
| `rules.csv` | AFL Tables, AFL and club articles | Average score in the season before and after each rule change |
| `waffle.csv` | AFL Tables | Share of 2026 games by state, as 100 squares |
| `states.csv` | AFL Tables, ABS | 2026 games, population and games per 100,000 residents by state |
| `venues.csv` | AFL Tables, Wikipedia | Games and average total score by venue, with coordinates |
| `flows.csv` | AFL Tables, Wikipedia | Team trips between cities by season since 2010 |
| `cities.csv` | Wikipedia | Coordinates for the city points on the flow map |
| `venue_sources.csv` | Wikipedia | The page used for each venue's coordinates |
| `aus_states.topojson` | Rowan Hogan | Simplified state boundaries |


## How the data was processed

- **Points:** goals × 6 + behinds. Season figures add both teams together.
- **Accuracy:** goals ÷ (goals + behinds).
- **Close game:** a win by fewer than 6 points.
- **Margins:** decades start at 1900 in the data files, and the charts show the 1950s onward. The ridgeline shapes use a Gaussian smoother with a 5-point bandwidth.
- **Venue averages:** the latest five seasons, leaving out 2020 (2022–2026), for venues with at least five games.
- **Rule comparisons:** one season before and one after each change. The 2021 change compares 2019 with 2021.

## Assumptions

- **The 2020 season:** quarters were shortened from 20 to 16 minutes, so it's left out of decade margins, venue averages and rule comparisons. It stays in `seasons.csv`, `team_season.csv` and `team_rank.csv`, and is shown separately where it's charted against other seasons.
- **Club names:** Footscray is counted as Western Bulldogs, South Melbourne as Sydney, Kangaroos as North Melbourne, and Brisbane Bears as Brisbane Lions.
- **Home cities:** assigned for this project. The Melbourne clubs are Carlton, Collingwood, Essendon, Hawthorn, Melbourne, North Melbourne, Richmond, St Kilda and Western Bulldogs. Geelong is its own city. Adelaide and Port Adelaide are Adelaide, Fremantle and West Coast are Perth, and Sydney and Greater Western Sydney are Sydney.
- **Team trips:** counted whenever a club plays in a different city from its home city, including Geelong to Melbourne. Six games played overseas since 2010 are left out.
- **Venue locations:** each venue was assigned to a city and state for this project.

## Checks

Season game counts and average scores up to 2024 were compared with a separate public copy of AFL Tables data (https://github.com/akareen/AFL-Data-Analysis). The only differences came from three finals missing from that copy.

## Licences

The ABS and Wikipedia publish their own reuse terms. No licence was seen on the AFL Tables page used or in the australian-states README, so all sources are credited here and on the page.

