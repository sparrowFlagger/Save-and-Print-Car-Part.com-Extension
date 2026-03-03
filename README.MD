# Car-Part.com Save & Print

A browser extension for Chrome and Firefox that adds save and print functionality to [car-part.com](https://car-part.com) search results. Save individual listings or your entire search as a clean, printable HTML report — complete with full-size photos, dealer info, and a link back to the original search.

Also available as a Tampermonkey userscript if you prefer not to install an extension.

---

## Screenshots

![Search results page with toolbar](ScreenShots/search-results.png)
![Exported report with photos](ScreenShots/report.png)

---

## Features

- **Per-row save** — Save any individual listing as a standalone HTML report, titled with the stock number
- **Bulk save** — Check multiple rows and save them all at once with a single click
- **Save Search Results** — Export the entire results page in one go
- **Full-size photos** — Automatically fetches photos from car-part.com and includes them in the report
- **Clean dealer info** — Strips out Request Quote / Insurance Quote / Live Chat links that serve no purpose in a saved report; keeps the dealer name and URL
- **Two-table layout** — Main part data on top, dealer info and distance on a second row so nothing gets cramped when printing
- **Back-link** — Every export includes a link back to the original search page
- **Settings** — Choose between Gallery, Full-size, or No images mode; preference is saved across sessions
- **CO2e text stripped** — car-part.com's promotional green text is removed from exports automatically
- **Print / Save as PDF** — Every export page includes a print button with clean print CSS

---

## Installation

### Chrome / Edge

1. Download and unzip `save-and-print-chrome.zip`
2. Go to `chrome://extensions`
3. Enable **Developer mode** (toggle in the top right)
4. Click **Load unpacked** and select the unzipped folder
5. Navigate to a car-part.com search — the toolbar will appear above the results

### Firefox

**Option A — Install via XPI (recommended):**
1. Download `Save-and-Print_Car-Part.com_firefox.xpi`
2. Go to `about:addons`
3. Click the gear icon → **Install Add-on From File**
4. Select the `.xpi` file
5. Right-click the Firefox toolbar to pin the extension icon

**Option B — Load manually:**
1. Download and unzip `save-and-print-firefox.zip`
2. Go to `about:debugging` → **This Firefox**
3. Click **Load Temporary Add-on**
4. Select the `manifest.json` file inside the unzipped folder

> **Note:** If using regular Firefox, go to `about:config` and set `xpinstall.signatures.required` to `false` for a stable permanent install without needing Developer Edition.

### Tampermonkey (any browser)

1. Install [Tampermonkey](https://www.tampermonkey.net/) for your browser
2. Download and unzip `save-and-print-tampermonkey.zip`
3. Open Tampermonkey → **Create a new script**
4. Paste in the contents of the `.user.js` file and save

---

## How to Use

Once installed, a toolbar panel appears above the results table on any car-part.com search page:

```
+------------------------------------------------------------------+
| Car-Part.com Save & Print         Search: 2019 VW Golf Wheel     |
+------------------------------------------------------------------+
| Settings (Gallery)   Save Selected (0)   Save Search Results     |
+------------------------------------------------------------------+
```

### Saving a single listing

Each result row has a **Save #[Stock#]** button on the right. Click it to fetch photos and open the report in a new tab. Rows with photos show a blue button; rows without show grey.

### Saving multiple listings

Check the checkbox next to each row you want, then click **Save Selected (N)**. Each selected row opens as its own report tab.

### Saving the whole search

Click **Save Search Results** to export the entire results table as a single HTML page with thumbnail images.

### Settings

Click **Settings** to choose the default image mode:

| Mode | Description |
|------|-------------|
| **Gallery** | Compact grid layout — recommended for most uses |
| **Full-size** | Large stacked images — best for detailed inspection |
| **No images** | Text only — fastest, works fully offline |

---

## Report Layout

```
Stock #23JA018A - 2019 Volkswagen Golf Wheel
Original Search: 2019 Volkswagen Golf Wheel  |  Saved: 3/2/2026

<- Back to original search on car-part.com

+-------------------------------------------------------------+
| Year/Part/Model | Description | Damage | Grade | Stock# | Price |
| 2019 VW Golf    | SUN S       | 000    | A/0   | 23JA.. | $150  |
+-------------------------------------------------------------+

+-------------------------------------------------------------+
| Dealer Info                               | Dist mile       |
| A & L Auto Parts (http://trade5969...)    | 471             |
+-------------------------------------------------------------+

[ Mode: Gallery ]

[ photo ]  [ photo ]  [ photo ]  [ photo ]  [ photo ]
[ photo ]  [ photo ]  [ photo ]  [ photo ]
```

---

## Files

| File | Description |
|------|-------------|
| `save-and-print-chrome.zip` | Chrome / Edge extension (Manifest V3) |
| `save-and-print-firefox.zip` | Firefox extension source (Manifest V2) |
| `Save-and-Print_Car-Part.com_firefox.xpi` | Firefox extension packaged for direct install |
| `save-and-print-tampermonkey.zip` | Tampermonkey userscript |

---

## Technical Notes

- **CORS** — Photo fetching hits `imageappoh.car-part.com` which blocks cross-origin requests from page context. The extension routes these fetches through a background service worker (Chrome) / background script (Firefox) which bypasses CORS restrictions.
- **Storage** — Chrome uses `chrome.storage.sync`; Firefox uses `browser.storage.local` for reliability without requiring sign-in.
- **Manifest versions** — Chrome uses Manifest V3; Firefox uses Manifest V2.
- **Tampermonkey** — Uses `GM_xmlhttpRequest` for photo fetching (bypasses CORS natively) and `GM_setValue` / `GM_getValue` for settings.
- **ASCII only** — The Firefox content script is strictly ASCII to avoid Firefox's stricter JS character handling.

---

## License

MIT
