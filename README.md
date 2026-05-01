# UEFA Champions League & Domestic League Performance Impact

This is an ongoing data science project where I’m trying to explore whether playing in the UEFA Champions League has any measurable impact on domestic league performance.

The general idea is simple: when teams play in the Champions League, they deal with more congested fixtures, travel, and higher intensity schedules — and I want to see if this actually affects their league results, and if it does, how much it affects them (e.g., changes in average points after CL matches, short-term performance drops, etc.).

---

## What I’m Trying to Explore

At a high level, I want to understand:

- Do teams perform worse in their domestic leagues after Champions League matches?
- Does playing in the Champions League season overall affect league performance?
- Does deeper progression in the CL make the effect stronger?
- Do high Elo teams perform differently compared to low Elo teams in terms of handling fixture congestion?

This is more of an exploratory analysis rather than a strict academic study.

---

## Data

I’m working with:

- Domestic league match data (5 major leagues + Turkish Super League)
- UEFA Champions League match data
- Exactly 6 seasons per league
- Elo ratings dataset (for team strength context, available up to 2025-06-01; the last season will be treated without Elo where necessary)

All match data was collected from:  
https://fixturedownload.com  

Elo ratings dataset:  
https://www.kaggle.com/datasets/adamgbor/club-football-match-data-2000-2025  

---

## What I Plan to Do

### 1. Data Cleaning & Preparation

I’m planning to merge everything into a unified match-level dataset with the following structure:

- team  
- opponent  
- date  
- competition  
- season  
- is_home  
- goals_for  
- goals_against  
- points  
- stage  
- ucl_format  
- match_number  
- team_elo  
- opponent_elo  
- elo_diff  

---

### 2. Feature Engineering

Not fully defined yet. I’ll design this step iteratively while building the dataset and running initial analysis.

---

### 3. Analysis

This will be defined later after cleaning and merging is complete.

---

## Methods I might use

Also not finalized yet. I’ll decide based on the structure of the cleaned dataset.

Right now, the priority is completing the data preparation and merging pipeline first.

---

## Why I’m Doing This

Mainly out of curiosity and interest in football analytics.

The goal is to build a structured dataset and analysis pipeline that can later be extended into deeper sports analytics questions.

---

## Status

This project is in the early development stage.

Current focus:
- data cleaning
- dataset merging
- building a unified match-level dataset