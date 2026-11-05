# exPrice: currency converter on hover & right-click (Chromium / Dia)

Highlight a price on any web page, right-click it, and the context menu shows a row like:

    $1,299.99 USD ≈ €1,195.40 EUR

Rest the mouse on any price and a small bubble shows the converted amount right next to it, with a copy button. That
works even when a site splits a price across several elements, like Amazon's `$` `29` `.99`. The bubble can also appear
when you highlight a price; that option is off by default. Both are toggles in settings. Clicking the menu row or the
bubble's copy button copies the converted amount (configurable).

## Install (Dia, Chrome, Edge, Brave, Arc…)

1. Open `chrome://extensions` (in Dia you can also reach it from the menu: Extensions → Manage Extensions).
2. Turn on **Developer mode** (top-right).
3. Click **Load unpacked** and choose the `extension/` folder.
4. The settings page opens. Pick your currency under **Convert to**.

Pages that were open before installing are wired up automatically. To also convert in local `file://` pages, turn on
"Allow access to file URLs" in the extension's details.

## What it detects

- Symbols before or after the number: `$5`, `5 €`, `£20`, `¥1,000`, `₪49.90`, `R$ 1.500,00`, `12,50 zł`, `250 Kč`, `100 kr`, `US $25`, `CA$10`, `HK$88`…
- ISO codes: `USD 100`, `100 EUR`, `1.000,50 CHF`, `100 usd`
- Written names: `20 dollars`, `5 euros`, `300 Swiss francs`, `100 shekels`, `1,000 yen`
- Number formats: `1,234.56`, `1.234,56`, `1 234,56`, `1'234.50`, `1,23,456` (Indian), `.99`
- Magnitudes: `$5k`, `$1.5M`, `$2 billion`, `€3 Mrd.`, `₹5 crore`, `₹2 lakh`
- Negative amounts: `-$5`, `−5 €`. Ranges like `10-20 EUR` are not read as negative.

Symbols shared by several currencies (`$`, `¥`, `kr`, `Rs`) default to **Auto**: the site's country domain decides
(`$` on amazon.ca → CAD, `¥` on a .cn site → CNY), otherwise USD / JPY / SEK / INR. You can change each one in settings.

## Exchange rates

Downloaded from [ExchangeRate-API](https://www.exchangerate-api.com) (no key needed), with
[fawazahmed0/exchange-api](https://github.com/fawazahmed0/exchange-api) as fallback. Rates are cached locally and refreshed every 6
hours. The cached rates keep working offline.

## Limitations

- Chrome extensions can't change a context menu after it opens, so the row is computed as you select. Highlight first, then right-click.
- Browser-internal pages (`chrome://`, the Web Store, the built-in PDF viewer) don't allow extensions, so the row doesn't appear there.
- When a selection contains several amounts, the first one is converted. Selections over 200 characters are ignored.

## Development

    LANG=en_US.UTF-8 node tests/parser.test.mjs      # detection + formatting tests
    LANG=en_US.UTF-8 node tests/background.sim.mjs   # service-worker flow against a mocked chrome.* API

(`LANG` pins number formatting so the expected strings match on any machine.)
    python3 tools/make_icons.py extension/icons
