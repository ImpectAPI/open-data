# IMPECT Open Data <picture><source media="(prefers-color-scheme: dark)" srcset="https://github.com/ImpectAPI/open-data/blob/main/img/impect_logo_white.svg"><source media="(prefers-color-scheme: light)" srcset="https://github.com/ImpectAPI/open-data/blob/main/img/impect_logo_black.svg"><img alt="Impect Logo" src="https://github.com/ImpectAPI/open-data/blob/main/img/impect_logo_white.svg" align="right" height="40"></picture>

This repository provides open-access football event data from **Impect**, a leading provider of football analytics and event data. The dataset includes detailed match event data, focusing on key performance indicators such as bypassed opponents and other advanced metrics.

## Dataset Overview

- **Source**: [Impect](https://www.impect.com)
- **Format**: JSON
- **Coverage**:
  - Bundesliga 2023/24
- **Data Points**:
  - Event Data
  - Event KPIs
  - Player KPIs (Match Aggregates)
  - Team Lineups & Substitutions
  - Match Info
  - Player Info
  - Squad Info
  - Country List
  - Iteration List
  - KPI Definitions

## How to Use the Data

1. **Clone the Repository**
   ```sh
   git clone https://github.com/ImpectAPI/open-data.git
   ```
2. **Navigate to the Project Folder**
   ```sh
   cd open-data
   ```
3. **Load Data in Python (Example)**
   ```python
   import pandas as pd
   
   # read data
   df = pd.read_json("data/events/events_122838.json")
   
   # print first 5 rows to console
   print(df.head())
   ```

## How to Use the Data with [Kloppy](https://kloppy.pysport.org/)

[Kloppy](https://kloppy.pysport.org/) by [PySport](https://pysport.org/) is _the_ industry standard open-source fooball data standardization package. Kloppy simplifies football data processing by offering a single place to [**load**](https://kloppy.pysport.org/user-guide/loading-data/impect/), [**filter**](https://kloppy.pysport.org/user-guide/getting-started/#filtering-data), [**transform**](https://kloppy.pysport.org/user-guide/transformations/coordinates/) and [**export**](https://kloppy.pysport.org/user-guide/exporting-data/) your football data in a standardized way. 

To get started with the open dataset simply,
 
1. **Install Kloppy**
   ```sh
   pip install kloppy>=3.18.0
   ```
   
2. **Load the data**
   ```python
   from kloppy import impect

   events = impect.load_open_data(match_id=122840)
   ```

   To load other, non-open data use `impect.load()` instead.

3. **Filter, Transform and Export**
    ```python
    df = (
        events.transform(
            to_orientation="STATIC_HOME_AWAY"
        )  # now, the home team always attacks left to right
        .filter(lambda event: event.period.id == 1)  # only keep frames from the first half
        .to_df(
            engine="polars"
        )  # convert to a Polars DataFrame, or use engine="pandas" for a Pandas DataFrame
    )
    ```

## Data Structure

The dataset is organized as follows:

```
open-data/
│-- data/
│   │-- events/               # Contains all in-game events. The filename contains the match ID.
│   │-- events_kpis/          # KPIs on event level for the above event data. The filename contains the match ID.
│   │-- lineups/              # Team lineups and substitutions. The filename contains the match ID.
│   │-- matches/              # Match metadata. The filename contains the iteration ID.
│   │-- player_kpis/          # KPI aggregates per player per position per match including play duration. The filename contains the match ID.
│   │-- players/              # Player master data. The filename contains the iteration ID.
│   │-- squads/               # Squad master data. The filename contains the iteration ID.
│   │-- countries.json        # List of countries.
│   │-- iterations.json       # Iterations of competitions.
│   │-- kpi_definitions.json  # Definitions of key performance indicators (KPIs).
```

For detailed information on data structure and format, please refer to [`Documentation.pdf`](https://github.com/ImpectAPI/open-data/tree/main/Documentation.pdf).

## Licensing & Attribution

- By using this data you agree to our terms and conditions. See [`LICENSE.pdf`](https://github.com/ImpectAPI/open-data/tree/main/LICENSE.pdf) for the full terms and conditions.
- If you use this data in your research or projects, please credit **Impect** as the data provider and use our logo from the [`img`](https://github.com/ImpectAPI/open-data/tree/main/img) folder.

## Share Your Work!

We encourage users to publish their work using this dataset! Whether it's a blog post, a research paper, a visualization, or an analysis, we'd love to see how you're using the data. Tag Impect on social media to share your insights:

- **X (formerly Twitter):** [@impect_official](https://x.com/impect_official)
- **BlueSky:** [@impect-official.bsky.social](https://bsky.app/profile/impect-official.bsky.social)
- **LinkedIn:** [Impect on LinkedIn](https://www.linkedin.com/company/impect-gmbh)

Join the community and showcase your findings to fellow analysts, researchers, and football enthusiasts!

## Contribution

We welcome contributions to improve data accessibility and documentation! Feel free to submit pull requests or report issues in the [Issues](https://github.com/your-username/impect-open-data/issues) section.

## Contact

For any inquiries regarding this dataset, please reach out to:
- **Impect Website**: [www.impect.com](https://www.impect.com)
- **Email**: [thomas.walentin@impect.com](mailto:thomas.walentin@impect.com)
- **Email**: [florian.schmitt@impect.com](mailto:florian.schmitt@impect.com)

---

🚀 *Happy Analyzing!*