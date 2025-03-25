# Media Scraper

`media-scraper` scrapes all photos and videos from web pages.  
It supports general-purpose scraping as well as SNS-specific scrapers like Instagram and Twitter.

---

## 🆕 Modernization & Improvements (2025)

This project has been revived and updated with modern tooling and compatibility:

### ✅ Highlights

- **Selenium 4 Compatibility**  
  Replaced deprecated `executable_path`, `desired_capabilities`, etc. with the modern `Service` API.
  
- **Uses `chromedriver` from System PATH**  
  Automatically picks up your installed ChromeDriver, no need to hardcode versions or manage local copies.

- **Recursive Scraping (up to 3 levels deep)**  
  New method `scrape_recursive()` allows the scraper to follow all links on a page up to 3 levels deep and download media from each page visited.

- **Windows-Safe Filenames and Folders**  
  Sanitizes folder names derived from `<title>` to strip characters not allowed by Windows (`<>:"/\\|?*`), and trims trailing spaces/dots.

- **Automatic Folder Creation**  
  Ensures folders exist before saving, preventing crashes due to missing or invalid paths.

---

This modernization work was contributed by [@mitchlinDEV](https://github.com/mitchlinDEV), with assistance from [ChatGPT](https://chat.openai.com/) to help debug, refactor, and extend functionality.

---

## General-purpose Scraping

The general scraper downloads all photos and videos from:

- `<a href=...>` links that point to media files
- `<img src=...>` image tags
- `<video src=...>` video tags

---

## SNS-specific Scrapers

Currently supported:

- **Instagram**: Downloads all posts from a given username.
- **Twitter**: Downloads all media tweets from a given username.

---

## Usage

General web page media scraping:
```bash
python3 -m mediascraper.general [URL1 URL2 ...]
```

Recursive scrape up to 3 levels deep (default behavior now):
```bash
python3 -m mediascraper.general https://example.com
```

Media will be stored in `download/general`.

Scraping Instagram:
```bash
python3 -m mediascraper.instagram [USERNAME1 USERNAME2 ...]
```

Scraping Twitter:
```bash
python3 -m mediascraper.twitter [USERNAME1 USERNAME2 ...]
```

---

## Installation

```bash
git clone https://github.com/mitchlinDEV/media-scraper.git
cd media-scraper
pip install -r requirements.txt
```

### Requirements

- Python 3.6+
- Chrome browser
- Chromedriver installed and added to your system `PATH`

---

## Login with Credentials

If you want to scrape media that requires login (e.g. private Instagram), rename and fill out:

```bash
cp credentials.json.example credentials.json
vim credentials.json
```

Then run with:
```bash
python3 -m mediascraper.instagram USERNAME -c credentials.json
```

---

## Parameters

| Parameter      | Description                                 | Default    |
|----------------|---------------------------------------------|------------|
| `scroll_pause` | Pause time during scroll automation         | `0.5s`     |
| `mode`         | `'silent'`, `'normal'`, or `'verbose'`      | `'normal'` |
| `debug`        | Save debug pages, print URLs to console     | `False`    |

---

## How to Extend

- `MediaScraper` includes a `scrape_recursive()` method for depth-based crawling.
- You can subclass `Scraper` to build support for more platforms (like Reddit, TikTok, etc.)

---

## Known Limitations

- Twitter video scraping may fail if content uses blob URLs (though m3u8 parsing is supported).
- Instagram’s API changes frequently and may require updated selectors.

---

## Credits

Originally by [Elvis Yu-Jing Lin](https://github.com/elvisyjlin)  
Modernized & extended by [@mitchlinDEV](https://github.com/mitchlinDEV)  
Readability, upgrades, and bad joke filtering by [ChatGPT](https://chat.openai.com/)
