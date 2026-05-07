# UEFA Champions League & Domestic League Performance Impact

This is an ongoing data science project where I’m trying to explore whether playing in the UEFA Champions League has any measurable impact on domestic league performance.

The general idea is simple: when teams play in the Champions League, they deal with more congested fixtures, travel, and higher intensity schedules — and I want to see if this actually affects their league results, and if it does, how much it affects them (e.g., changes in average points after CL matches, short-term performance drops, etc.).

---

## What I’m Trying to Explore

At a high level, I want to understand:

- Do teams perform worse in their domestic leagues after Champions League matches?
- Does playing in the Champions League season overall affect league performance?
- Does deeper progression in the CL make the effect stronger?
- How does league performance vary based on recovery time after Champions League matches (0–3 days, 4–6 days, 7+ days)?
- Is the decline (if any) after Champions League matches more pronounced in away games?
- Do elite teams resist the effect (if any) of playing in the Champions League?
- Does the goal scoring / conceding ability of teams change after playing in the Champions League?
- Does new UCL format increase fatigue?

This is more of an exploratory analysis rather than a strict academic study.

---

## Data

I’m working with:

- Domestic league match data (5 major leagues + Turkish Super League)
- UEFA Champions League match data
- Exactly 6 seasons per league

All match data was collected from:  
https://fixturedownload.com  

---

## What I Plan to Do

### 1. Data Cleaning & Preparation

The raw data consisted of individual CSV files for six domestic leagues and the UEFA Champions League across six seasons (2020–2026). The preparation pipeline was designed to transform this fragmented data into a unified, team-centric dataset.

#### Data Integration & Standardization

Raw files were ingested by parsing season information from filenames and standardizing column names across all competitions. Unnecessary metadata such as match locations and group stage markers were pruned to focus on performance metrics.

#### Team Name Normalization

A rigorous normalization mapping was implemented to resolve naming inconsistencies across different data sources (e.g., unifying `"Bayern"`, `"FC Bayern"`, `"FC Bayern München"` and `"Bayern München"` into a single entity). This was critical for accurate merging and longitudinal tracking of team performance.

#### Perspective Transformation (Team-Centric Modeling)

To analyze performance from a specific team's point of view, the match-level data was duplicated and mirrored. Each match is represented twice:

- Once where the home team is the `target_team`
- Once where the away team is the `target_team`

This allows for a continuous chronological timeline of matches for every participant.

#### Dataset Pruning & Noise Reduction

The dataset was filtered to include only **UCL Participants** — teams that competed in the Champions League at least once during the study period.

This process successfully reduced the dataset size by approximately **41%**, eliminating noise from teams irrelevant to the research question while retaining **100%** of the relevant league and European matches for the target teams.

---

### 2. Feature Engineering

To quantify the **"UCL Effect,"** several complex features were engineered to capture the temporal and physical demands placed on the squads.

#### Recovery Time Tracking (`days_since_last_ucl_match`)

Using a `merge_asof` logic, the pipeline identifies the exact date of a team's most recent Champions League fixture relative to their current domestic match.

This calculates the precise number of recovery days available between European and league play.

#### Impact Categorization (`ucl_impact_category`)

Teams are classified into three fatigue tiers based on their recovery window:

- **Severe:** Domestic match occurs $\leq 3$ days after a UCL match.
- **Moderate:** Domestic match occurs within 4–6 days.
- **No Effect:** Domestic match occurs $> 6$ days after, or with no prior UCL match in that window.

#### Accumulated Fatigue (`target_team_match_count`)

A cumulative counter tracks the total number of matches played by a team within a specific season.

This serves as a proxy for season-long physical wear and tear, allowing the analysis to distinguish between early-season freshness and late-season exhaustion.

#### Competitive Context

##### Points Calculation

Result strings were parsed into discrete goal counts to calculate domestic league points from the `target_team` perspective:

- **3 points** for a win
- **1 point** for a draw
- **0 points** for a loss

##### UCL Format Differentiation

A feature was added to distinguish between:

- The **"Old"** group stage format
- The **"New"** league phase format introduced in the 2024–2025 season

This enables a comparative study of how different European competition structures impact domestic success.

---

### 3. Analysis

The core analytical phase has been completed. The Exploratory Data Analysis (EDA) focused on answering the initial research questions by evaluating:

- **The General Impact:** Measuring the overall drop in domestic league Points Per Game (PPG) following Champions League fixtures.
- **Fatigue & Recovery:** Comparing team performance across different rest intervals (0–3 days, 4–6 days, and 7+ days).
- **Elite Team Resilience:** Assessing whether top-tier teams with deeper squads are more resistant to the "UCL Effect" compared to standard participants.
- **New vs. Old Format:** Evaluating the physical toll of the newly introduced 2024–2025 league phase format against the traditional group stage.
- **Home/Away & Goal Dynamics:** Analyzing if post-UCL performance drops are more severe in away games and how goal scoring/conceding trends shift.

*(Detailed statistical findings and visualizations will be published in the upcoming final report.)*

---

## Methods I Used

- **Python (Pandas, NumPy):** Extensively used for data ingestion, cleaning, and complex transformations. Functions like `merge_asof` were crucial for accurately mapping the timeline between European and domestic fixtures to calculate exact recovery days.
- **Exploratory Data Analysis (EDA):** Conducted within Jupyter Notebooks to investigate distributions, calculate performance variations, and uncover statistical trends.
- **Feature Engineering:** Developed custom metrics including cumulative match loads to measure seasonal fatigue, and impact categorization based on recovery windows.
- **Data Visualization:** Utilized data visualization tools to visually map performance drops, home/away discrepancies, and differences between team tiers.

---

## Why I’m Doing This

Mainly out of curiosity and interest in football analytics.

The goal is to build a structured dataset and analysis pipeline that can later be extended into deeper sports analytics questions.

---

## Status

**Almost Complete.**

The data collection, processing, and analytical phases are entirely finished. Currently, final checks and code validations are being conducted. Once these final verifications are complete, a comprehensive final report detailing all findings will be written.