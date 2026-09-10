# BOL Splitter (web)

Splits scanned Bill-of-Lading PDFs by page, reads each page's PO number using
Google's Gemini API, renames the page to that PO number, and zips all pages
from one source PDF together — entirely in your browser. No install, no
server, no Python.

## Use it

Open the live page (GitHub Pages URL for this repo), then:

1. Paste in a free Gemini API key — get one at [aistudio.google.com](https://aistudio.google.com) ("Get API key"). It's only stored in your own browser (`localStorage`) if you check "Remember", and is never sent anywhere except directly to Google's API.
2. Choose one or more scanned BOL PDFs.
3. Click **Split & Zip**. A zip (one per source PDF) plus a `manifest.csv` download automatically.

Pages the model can't confidently read come back as `PAGE_n_UNREADABLE.pdf`
inside the zip and are flagged `REVIEW` in the manifest — never silently
guessed wrong.

## Notes

- Requires internet access (calls the Gemini API directly from your browser).
- Google's free tier has a daily request cap — fine for occasional batches.
- Everything (PDF splitting, zipping) happens client-side via [pdf-lib](https://pdf-lib.js.org/) and [JSZip](https://stuk.github.io/jszip/); only the PDF bytes are sent to Google for reading.
- Calibrated for Amazon Freight BOL templates (see the prompt in `index.html` for the exact template definitions it looks for). Other layouts will mostly come back `UNREADABLE` rather than a wrong guess.
