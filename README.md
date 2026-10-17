# Egypt CPI Inflation Dashboard

Responsive static dashboard for Egypt's CPI index-point database. The page fetches the source CSV directly from GitHub, so monthly data updates do not require editing the code.

## Files
- `index.html` — page structure and library imports
- `style.css` — responsive layout and CIB-inspired blue/orange theme
- `script.js` — CSV loading, inflation calculations, category cards and charts

## Run locally
Browsers may restrict fetching remote data from a `file://` URL. Use a local static server:
- VS Code: run `index.html` with Live Server
- Python: `python -m http.server 8000` in this folder, then open `http://localhost:8000`

## Publish
Upload these files to the repository (or a separate dashboard repository) and enable GitHub Pages. The data source is:
`https://raw.githubusercontent.com/o-elkaraksy/Inflation_dashboard_OCT2026/refs/heads/main/dashboard_data.csv`

## Data assumptions
- The first three CSV columns are `category family`, `Category`, and `Weights Rebased`; monthly CPI index columns follow and use labels such as `Jan-21`.
- The current CSV uses labels such as `main category 1`, `sub category 1.1`, and `sub item 1.1`. Sub-item family codes may identify their parent subcategory directly (rather than adding another numeric level); the dashboard groups items by the parent code and preserves source order.
- YoY and MoM inflation are calculated from CPI index points. YoY is unavailable until January 2022 and MoM is unavailable for the first observation.
- “All Items” is treated as the headline aggregate, not a separate category card or contributor.
- Main-category contribution uses the rebased main-category weight × category index change ÷ previous-period All Items index. Sub-item contribution uses the sub-items weight × item index change ÷ previous-period index of its selected main category. Contributions are not proportionally reconciled. The contribution chart shows component contributions in percentage points and labels each column with the headline or selected category inflation rate. This is an analytical decomposition, not an official statistical contribution series.
- The historical category panel uses checkboxes to select additional series. “All data” chart ranges begin in January 2022.

## Monthly update
Add the new month CPI index column to `dashboard_data.csv`, preserve the metadata columns and hierarchy labels, commit the CSV to GitHub, and refresh the dashboard. No CPI observations are hardcoded in the JavaScript.

## Standalone HTML
`egypt_cpi_dashboard_standalone.html` combines the HTML, CSS, and JavaScript in one file. It fetches the latest CSV and loads chart libraries from CDNs, so internet access is required. If a browser blocks remote fetches from a local file, use the three-file version with a local static server.


## Updated UI
The historical modal now plots only the selected main category. Contribution analysis is simplified to main categories or the two selected parent categories. Period sliders mirror the quick range buttons. The standalone file still requires an internet connection for CDN libraries and the GitHub CSV.
