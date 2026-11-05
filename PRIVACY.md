# Privacy Policy — exPrice

_Last updated: 2026-11-05_

**exPrice does not collect, store, sell, or share any personal data.**

## What the extension processes

- **Selected and hovered text.** When you highlight text, or rest the mouse on text, the extension reads that text
  (at most a short snippet around the pointer) inside your browser to detect a price and show the converted amount. It
  never sends, logs, or keeps this text.
- **Website domain.** The page's domain (for example `amazon.ca`) is checked locally to tell shared symbols apart
  (for example `$` meaning Canadian dollars). It never leaves your browser.
- **Settings.** Your target currency and preferences are kept in Chrome's extension storage. If Chrome Sync is on, Chrome
  syncs them between your own devices.

## Network requests

The extension downloads public exchange-rate tables from:

- `open.er-api.com` (ExchangeRate-API)
- `cdn.jsdelivr.net` and `latest.currency-api.pages.dev` (fawazahmed0/exchange-api), used only as a fallback

These requests contain no personal data, browsing data, or selected text. They fetch one fixed file listing rates against the US dollar.
Like any web request, they reveal your IP address to those services, which their own privacy policies cover.

## Clipboard

When you click the converted amount in the right-click menu, or the copy button in the bubble, the extension writes that
amount to your clipboard. It never reads your clipboard.

## Contact

Questions: exprice.dev@gmail.com
