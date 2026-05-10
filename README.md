# Audience-Analytics
The final of the three analytics projects to understand what makes a movie work; through the exploration and examination of how the audience perceved the movie.

# 🎬 Audience Ratings Behaviour
### May Newsletter — Movie Intelligence Series (Part 3 of 3)

A three-notebook investigation into whether audiences actually agree with the box office —
and the surprising answer that ties the whole series together. Using 100,000 MovieLens user
ratings bridged to the TMDB financial universe established in Parts 1 and 2, this project
measures the gap between commercial success and genuine audience satisfaction.

This is the final analytical instalment of the May newsletter series. The capstone predictive
intelligence project, combining all three datasets into a single ML pipeline, follows separately.

---

## 📊 Datasets

**Source:** [TMDB Movies Dataset](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset) via Kaggle

| File | Rows | Key Fields |
|------|------|------------|
| `ratings_small.csv` | 100,004 | `userId`, `movieId` (MovieLens ID), `rating` (0.5–5.0), `timestamp` |
| `links.csv` | 45,843 | `movieId` (MovieLens), `imdbId`, `tmdbId` — the bridge table |
| `movies_clean.parquet` | ~4,800 | Carried over from Part 1 |

The join chain is: `ratings_small → links (movieId → tmdbId) → movies_clean (id)`.
The `links.csv` file is the critical bridge — without it, the MovieLens rating universe
and the TMDB financial universe cannot be connected.

> `ratings_small.csv` and `links.csv` are not committed to this repo due to file size.
> Download them from the Kaggle link above and upload them to your Colab session alongside
> `movies_clean.parquet` before running.

---

## 🚀 Running the Notebooks

The notebooks must be run in order. NB9_Extended_Insights.ipynb can be run independently
after NB7, as it includes a self-contained data rebuild at the top of the setup cell.

**Step 1 — Upload the data**  
Upload `ratings_small.csv`, `links.csv`, and `movies_clean.parquet` to the Colab session.

**Step 2 — Run NB7**  
Constructs the join chain, aggregates 100k ratings to film level, engineers behavioural
features (`avg_user_rating`, `rating_std`, `rating_count`, `comm_vs_audience_gap`),
classifies each film into one of four archetypes, and saves `audience_clean.parquet`.

**Step 3 — Run NB8**  
Performs the full audience behaviour analysis — correlations, genre polarisation,
quadrant breakdowns, hidden gems, and overhyped films.

**Step 4 — Run NB9**  
Generates six summary visualisations for the newsletter.

**Step 5 — Run NB9_Extended_Insights**  
Generates six additional data-driven figures built around specific quantified findings.
This is the recommended source for the newsletter's analytical centrepieces.

---

## 🔍 Questions Explored

- Does box office revenue predict audience satisfaction? (Short answer: barely — r ≈ −0.02)
- Does *financial efficiency* (ROI) predict audience satisfaction? (Yes, meaningfully — monotonic staircase)
- Do older films genuinely rate higher, or is this survivor bias?
- Does a film gathering more ratings tend to score higher, and why?
- Which genres polarise audiences most — and which achieve consensus?
- Where do the TMDB community score and MovieLens user ratings most disagree?
- Which films are hidden gems (low revenue, high rating) and which are overhyped (high revenue, low rating)?

---

## 📐 Key Findings

| Finding | Statistic |
|---------|-----------|
| Revenue vs audience rating | r = −0.02 (virtually no relationship) |
| ROI vs audience rating | Monotonic — flops avg 3.33, smash hits avg 3.69 |
| Crowd wisdom effect | r = 0.34 between log(rating count) and avg rating |
| Survivor bias | 1960s avg rating 3.85 vs 1990s avg rating 3.33; n=57 vs n=554 |
| System agreement | TMDB vote average vs MovieLens rating r = 0.84 |
| Most polarising genre | Horror (avg rating std dev highest) |
| Most consensus genre | Drama (highest avg rating, lowest polarisation) |

---

## 🎭 Film Archetypes

Each film in the analysis-ready subset is classified into one of four quadrants based on
median splits of revenue and audience rating:

| Archetype | Revenue | Audience Rating |
|-----------|---------|-----------------|
| **Blockbuster** | High | High |
| **Hidden Gem** | Low | High |
| **Overhyped** | High | Low |
| **Critical Failure** | Low | Low |

---

## 📦 Intermediate Outputs

| File | Description |
|------|-------------|
| `audience_clean.parquet` | Film-level table with all financial fields plus aggregated audience metrics, quadrant classification, and polarisation tier |

---

## 🎨 Visual Style

Consistent with Parts 1 and 2 throughout, with one addition for the extended figures:

| Role | Colour |
|------|--------|
| Primary bars / lines | Midnight Navy `#1a1a2e` |
| Highlights / top performers | Oscar Gold `#e8b94f` |
| Warnings / contrast | Cinema Crimson `#c0392b` |
| Neutral fills | Silver `#bdc3c7` |
| Hidden gems / positive divergence | Teal `#1abc9c` |

---

## 📦 Dependencies

All standard libraries — no special installs required in Colab.

```
pandas
numpy
matplotlib
scipy
pyarrow      # for parquet read/write
```

---

## 🗺️ Series Roadmap

| Part | Focus | Status |
|------|-------|--------|
| 1 — Financial Performance | Genre ROI, budget tiers, seasonal patterns | ✅ Complete |
| 2 — Cast, Crew & Keywords | Director ROI, actor profitability, keyword analysis | ✅ Complete |
| **3 — Audience Ratings Behaviour** | Commercial success vs audience satisfaction | ✅ Complete |
| Final — Predictive Intelligence | ML model combining all three layers | 🔜 Coming |

---
