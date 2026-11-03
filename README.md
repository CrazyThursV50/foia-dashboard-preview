# Federal FOIA Dashboard (prototype preview)

A temporary preview of the BU Spark! DS 701 prototype dashboard for MuckRock's Data Liberation Project, so the team can try it in a browser. Not an official MuckRock product. The official version will be published from the team repository (BU-Spark/ds-muckrock-liberation); this repository will be removed or archived then.

**Open the dashboard:** the GitHub Pages link in the "About" box of this repository.

## What is here
- `docs/`: the built page that GitHub Pages serves (`index.html`, its libraries, and the data file `data/foia.json`).
- `index.qmd`, `styles.css`, `assets/`, `_quarto.yml`: the dashboard source (Quarto dashboard with Observable JS charts).
- `prep.py`, `column_mapping.csv`, `requirements.txt`: build `data/foia.json` from the team repository's component table.
- `serve.py`: local preview server.
- `tests/`: browser checks (Playwright): `check_numbers.py` compares the numbers on the page with the component table (and first checks its agency totals against the agency-level table), `check_edges.py` opens every view under unusual settings.
- `deploy/dashboard.yml`: draft GitHub Actions workflow for the team repository (monthly rebuild and GitHub Pages).

## Data
foia.gov annual reports, from one table in the team repository: `fa26/dataset/component_level/component_master_no_03_06_11.csv` (rebuilt from the foia.gov API in PR #25, not merged yet). Agency totals are its Agency Overall rows; components are its component rows.

## Rebuild
```
pip install -r requirements.txt
python prep.py --components <team repo>/fa26/dataset/component_level/component_master_no_03_06_11.csv
quarto render
rm -rf docs && cp -R _site docs && touch docs/.nojekyll
```
To view it locally instead: `python serve.py`, then open http://127.0.0.1:8765/_site/index.html. Opening `index.html` directly from disk does not work: the charts load their data over http.
