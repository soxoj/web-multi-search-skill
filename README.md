# web-multi-search

An OpenClaw skill that searches the web across multiple search engines simultaneously using [async-search-scraper](https://github.com/soxoj/async-search-scraper).

## Supported engines

| Engine | Status |
|--------|--------|
| Bing | Working |
| Yahoo | Working |
| Startpage | Working |
| Aol | Working |
| Ask | Working |
| Torch | Requires TOR proxy |

## Install

```bash
pip install -r requirements.txt
pip install git+https://github.com/soxoj/async-search-scraper.git --no-deps
```

The library must be installed from the GitHub URL (not PyPI). Use `--no-deps` because the library pins `bs4` which is the wrong package name on PyPI; the actual dependencies (`beautifulsoup4`, `aiohttp`, etc.) are already in `requirements.txt`.

## Usage

```bash
# Search all working engines, 3 pages each, JSON output
python3 web_multi_search.py "your query"

# Specific engines, more pages
python3 web_multi_search.py "query" --engines bing,yahoo --pages 5

# CSV output, deduplicate by URL
python3 web_multi_search.py "query" --unique-urls --output csv

# Human-readable text output
python3 web_multi_search.py "query" --output text

# With proxy
python3 web_multi_search.py "query" --proxy socks5://127.0.0.1:9050
```

## Output

JSON (default) writes to stdout, progress/warnings go to stderr:

```json
[
  {
    "engine": "Bing",
    "host": "example.com",
    "link": "https://example.com/page",
    "title": "Page Title",
    "text": "Snippet text..."
  }
]
```

## License

MIT
