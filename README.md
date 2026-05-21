# Saily eSIM Platform Performance Analysis

This project analyzes the performance of a newly launched eSIM service across Android and iOS platforms. The focus is on conversion rate, Android eSIM compatibility, purchase funnel behavior, anomalies, and practical recommendations.

The analysis is intentionally kept as a working data analysis notebook rather than a polished dashboard.

## Assignment focus

The notebook answers the main assignment questions:

- calculate conversion rate and other relevant performance metrics;
- compare Android and iOS performance;
- account for Android eSIM compatibility;
- investigate anomalies in recent platform performance;
- build a purchase funnel from event data;
- provide recommendations and suggest additional data that would improve the analysis.

## Project structure

Recommended structure:

```text
.
├── eSIM_eda_saily.ipynb
├── README.md
├── requirements.txt
└── data/
    ├── sessions.csv
    └── events.csv
```

The notebook also supports loading `sessions.csv` and `events.csv` from the same folder as the notebook, so the `data/` folder is recommended but not strictly required.

## Data files

Expected input files:

- `sessions.csv` — session-level data with platform, country, eSIM compatibility, transaction, purchased plan, and billing information.
- `events.csv` — event-level data with session IDs, event names, selected plan destination, and selected quota.

Main join key:

```text
unique_session_id
```

Important note: `unique_session_id` is not treated as a perfect user identifier. The analysis uses a session-day grain where appropriate:

```text
session_date + unique_session_id
```

This avoids overstating repeated sessions across dates.

## How to run

Create and activate a virtual environment, then install dependencies:

```bash
python -m venv .venv
.venv\Scripts\activate     # Windows
# source .venv/bin/activate # macOS/Linux
pip install -r requirements.txt
```

Then open the notebook:

```bash
jupyter lab
```

or:

```bash
jupyter notebook
```

## Main methodology choices

- Conversion rate is calculated as purchases divided by session-days.
- Android is split into compatible and incompatible devices because compatibility directly affects purchasing ability.
- Funnel steps are based on event presence per session, not raw event counts, to avoid distortion from repeated clicks or abnormal sessions.
- Anomaly investigation compares performance before and after the observed iOS change period.
- Country-level contribution analysis is used to identify which geographies explain the largest performance movement.

## Key limitations

- The events table does not contain an event timestamp, so exact event ordering inside a session cannot be fully verified.
- The data does not include marketing source, campaign, app version, device model, payment method, or checkout error information.
- Some destinations are regions rather than countries, so destination-level interpretation should be handled carefully.
- The analysis identifies likely causes, but final root-cause confirmation would require additional product, marketing, and technical data.

