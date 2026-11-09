# YouTube Music Listening Analyzer

A Jupyter notebook for analyzing YouTube Music history exported through Google Takeout. It summarizes artists, tracks, and listening patterns over time, and optionally enriches artists with Last.fm tags.

## Requirements

- Python 3.10 or newer
- Jupyter Notebook or JupyterLab
- `pandas`, `matplotlib`, and `pylast`

Install the Python packages in your environment:

```bash
python -m pip install jupyter pandas matplotlib pylast
```

## Prepare your data

1. Export your YouTube history from [Google Takeout](https://takeout.google.com/).
2. Place the YouTube history JSON file in the project folder and name it `watch-history.json`.
3. The notebook keeps only entries whose header is `YouTube Music`.

The history export is personal data and is excluded from version control by `.gitignore`.

## Optional Last.fm enrichment

The notebook can add up to three top tags for each artist. Without credentials, it uses tags already present in the local cache and marks uncached artists as not requested.

To enable API lookups, create a `.env` file in the project folder with your Last.fm API credentials:

```dotenv
LASTFM_API_KEY=your_api_key
LASTFM_API_SECRET=your_api_secret
```

The notebook reads `.env` directly. Keep this file private; it is ignored by Git. Successful lookups and artists with no tags are saved in `lastfm_artist_tags_cache.json`, which is also ignored by Git. Failed requests are not cached, so they can be retried later.

You can optionally set the timezone used for time-based analysis:

```dotenv
LOCAL_TIMEZONE=America/Chicago
```

The default is `America/Chicago`.

## Run the analysis

From the project folder, launch Jupyter:

```bash
jupyter lab
```

Open **Music analyzer.ipynb** and run its cells from top to bottom. The notebook cleans the history, checks the prepared data, builds rankings and charts, and summarizes the results. Counts represent history entries; they do not indicate completed plays or listening duration.

## Files

- `Music analyzer.ipynb` — analysis workflow and visualizations
- `watch-history.json` — local Google Takeout input (not tracked)
- `lastfm_artist_tags_cache.json` — local Last.fm cache (not tracked)
- `.env` — optional local API credentials and timezone (not tracked)
