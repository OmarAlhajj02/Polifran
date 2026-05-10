# Polifran

A socio-political data science project that builds a unified panel dataset of French National Assembly (17th legislature) members and analyzes their Wikipedia attention dynamics throughout 2025.

---

## Overview

Polifran combines two data sources to study how public attention to French MPs evolves over time:

- **Wikipedia pageview time series:** daily view counts per MP for the full year 2025
- **Wikidata-derived attributes:** party/group affiliation, gender, and age for each MP

The result is a panel dataset of ~187,000 rows (500+ MPs × 365 days) enabling both static profiling and temporal analysis of political visibility.

---

## Repository Structure

| File | Description |
|---|---|
| `Data_construction.ipynb` | Builds the dataset by querying Wikidata for MP metadata and the Wikipedia Pageviews API for daily view counts, then merges them into a single CSV |
| `dataset.csv` | The final panel dataset (name, gender, age, group, date, views) |
| `Visbility_analysis.ipynb` | Static analysis of MP attributes: distributions of age, gender, group, and their relationships |
| `Temporal_analysis.ipynb` | Temporal analysis: seasonality, spike detection, burstiness, group-level attention dynamics over time |

---

## Dataset

**Columns:** `name`, `gender`, `age`, `group`, `date`, `views`

**Coverage:** All MPs of the 17th French National Assembly · January–December 2025 · Daily granularity

**Political groups covered:** RN, Renaissance, LFI, PS, LR, Écologiste, MoDem, Horizons, LIOT, UDR, GDR, Non-inscrits

---

## Analyses

### Visibility Analysis
Static, structural analysis of the MP panel:
- Age and gender distributions
- Group composition and size
- Cross-variable relationships (age by group, gender by group, etc.)

### Temporal Analysis
Time-series analysis of Wikipedia attention:
- Total and mean daily views over the year
- Seasonality by day of week and month
- Spike detection using z-scores (individual and collective)
- Bursty vs. steady MP classification via coefficient of variation
- Group-level burstiness distribution
- Weekly attention heatmap by group
- Top spike events and spike-day clustering
- Individual time series for the most-viewed MPs
- Group-level attention trends over time

---

## Key Findings

### From Visibility Analysis

**Attention is not democratic.**
Wikipedia visibility follows a brutal power law: Gini coefficient of **0.725**. The bottom 50% of MPs share less than 8% of total views; the top 10% capture 65%. Most MPs exist, in the public eye, only on paper.

**Four types of MP, one assembly.**
K-means clustering reveals four distinct profiles: Stars (4 MPs: Gabriel Attal, Marine Le Pen, Sophia Chikirou, Yaël Braun-Pivet), Visible (24 MPs with consistent year-round traffic), Spiky (60 MPs who surface briefly then vanish), and Invisible (425 MPs, 83% of the assembly). One parliament, four parallel realities.

**LFI punches above its weight and shares it. RN does the opposite.**
LFI generates more than twice its proportional seat share in views (visibility ratio: 2.05) and distributes that attention internally (within-group Gini: 0.656, lowest among major parties). RN, the largest group in the assembly, underperforms its seat share, concentrates 73% of its views in 10% of its MPs, and deposits 97 members into the Invisible cluster. Marine Le Pen alone sits at 121× her group's median. RN's strength is electoral; individually, its rank-and-file is Wikipedia-invisible.

**The gender gap hides in plain sight.**
No overall gender gap exists (Mann-Whitney p=0.867), but the aggregate conceals a sharper pattern. Young women start with higher visibility than young men, then lose it faster with age (Spearman r=−0.415 vs −0.285). The gender penalty is really an age penalty that hits women harder, with the two trend lines crossing around age 50–55. And 3 of the 4 Star MPs are women: those who break through do so decisively.

---

### From Temporal Analysis

**The French political calendar writes itself into the data.**
October 2025 averages **205 views/MP/day**, nearly 3× the August floor of 72, making it the undisputed attention peak of the year. The *rentrée politique* (September–October) dominates, driven by budget debates and parliamentary confrontations. September 8 is the most intense single day: **59 MPs spiked simultaneously**, a cross-party collective event marking a major national political moment.

**Bursty vs. steady: two fundamentally different ways to be visible.**
MPs split almost evenly between bursty (event-driven spikes, CV > 1.31) and steady (durable baseline attention). François Hollande is the steadiest MP in the dataset (CV: 0.37), with no single event able to meaningfully move his already-high baseline. Alexandra Martin (LR) is the burstiest (CV: 7.37), reaching a z-score of 18.9 on a single October day after being virtually invisible the rest of the year.

**Opposition parties spike harder when it matters.**
Group-level attention curves diverge sharply in fall and converge in summer. LFI and RN show the sharpest October peaks, consistent with their leading roles in no-confidence motions and budget opposition. In quiet periods, all groups fade equally; in politically charged ones, opposition parties gain disproportionate attention relative to their size.

**Most extreme attention events are one-day phenomena.**
The top 20 spike events by z-score are spread across 13 different MPs from 9 different groups, with no party monopolizing sudden visibility. October 16 alone accounts for 4 of the top 20 spikes across different groups simultaneously, pointing to a single day of major national news that briefly illuminated otherwise low-profile MPs before they returned to obscurity.

---

## Stack

- Python 3
- `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `scikit-learn`
- `requests` for API calls
- Wikidata SPARQL endpoint
- Wikimedia Pageviews REST API

---

## Author

[OmarAlhajj02](https://github.com/OmarAlhajj02)
