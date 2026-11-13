# HTML Web Scraper

A small Python scraper that downloads a static web page with Requests and pulls structured data out of its HTML with Beautiful Soup. It reads a sample job board and prints each listing's title, company, location, and apply link.

![Python](https://img.shields.io/badge/Python-3-3776AB?logo=python&logoColor=white)
![Requests](https://img.shields.io/badge/Requests-2CA5E0?logo=python&logoColor=white)
![Beautiful Soup](https://img.shields.io/badge/Beautiful%20Soup-4-59666C)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)

📖 **[Full Documentation](https://chrisraiz.github.io/HTML-Web-Scraper/)**: setup, a walkthrough of each step, sample output, and adapting it to other sites.

---

## Overview

Many websites send their content as plain HTML, so a single HTTP request returns everything on the page. This project shows the basic scraping workflow for those pages, one step at a time:

- **Download** the page with `requests.get()`
- **Parse** the HTML into a searchable tree with Beautiful Soup
- **Find** elements by `id`, by tag and class, and by the text they contain
- **Walk up the tree** from a matching heading to the job card that holds it
- **Extract** clean text and link `href` values

It targets [Fake Python Jobs](https://realpython.github.io/fake-jobs/), a practice site from Real Python with 100 sample listings, and filters them down to the 10 whose title mentions Python.

## What It Collects

| Field | Found with | Example |
|---|---|---|
| Title | `<h2 class="title">` | Senior Python Developer |
| Company | `<h3 class="company">` | Payne, Roberts and Davis |
| Location | `<p class="location">` | Stewartbury, AA |
| Apply link | Every `<a>` tag's `href` in the card | `realpython.github.io/fake-jobs/jobs/senior-python-developer-0.html` |

## Tech Stack

- **Python 3**
- **Requests**, for downloading the page
- **Beautiful Soup 4** with Python's built-in `html.parser`

## Getting Started

```bash
git clone https://github.com/ChrisRaiz/HTML-Web-Scraper.git
cd HTML-Web-Scraper

python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

pip install requests beautifulsoup4
```

Run `deactivate` to leave the virtual environment when you're done.

## Usage

```bash
python3 static_web_scraper.py
```

Everything is printed to the terminal. The script prints the raw page, then the parsed results, then every Python job's title, company, and location, and finally each Python job's links:

```
Senior Python Developer
Payne, Roberts and Davis
Stewartbury, AA

Apply Here: https://realpython.github.io/fake-jobs/jobs/senior-python-developer-0.html
```

To scrape a different site, change `URL` and the `id`, tag, and class names the script searches for. The [documentation](https://chrisraiz.github.io/HTML-Web-Scraper/#adapting) walks through how.

## Project Structure

```
.
├── static_web_scraper.py   # The scraper
├── docs/                   # Documentation site (GitHub Pages)
├── LICENSE
└── README.md
```

## Limitations

This scraper only works on **static** pages, where the data is already in the HTML the server sends. Pages that build their content with JavaScript after loading need a real browser instead. For that approach, see [WoWHead NPC Scraper](https://github.com/ChrisRaiz/WoWHead-NPC-Scraper), which uses Selenium.

## Disclaimer

This is a learning project. Fake Python Jobs is a practice site built for scraping tutorials. When scraping other websites, check their terms of service and `robots.txt`, and keep your request rate reasonable.

## License

Released under the [MIT License](LICENSE).
