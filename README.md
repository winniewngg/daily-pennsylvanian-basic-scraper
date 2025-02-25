# Daily Pennsylvanian Basic Scraper (Made From Basic Scraper Template)

This scraper was modified to extract the four featured headlines from the Featured section of The Daily Pennsylvanian homepage. Previously, it only retrieved a single main headline. The updated scraper now collects multiple headlines from a structured div container and saves them into a JSON file for historical tracking.

## Overview

The workflow defined in `.github/workflows/scrape.yaml` runs on a defined schedule to:

1. Checkout the code
2. Set up the Python environment
3. Install dependencies via Pipenv
4. Run the python script `script.py` to scrape data
5. Commit any updated data files to the Git repository

## Featured Headlines Scraping

The original scraper focused on a single headline from the homepage using frontpage-link. The updated version now finds all featured headlines within the __flexy-box container, which houses special-edition divs. Instead of stopping at the first found link, the scraper now iterates through up to four articles (which is exactly how many featured headlines there are). Each special-edition div contains a frontpage-link standard-link, which is now correctly parsed to retrieve multiple headlines. Instead of returning a single string, the scraper now returns a dictionary where each headline is indexed (Featured_1, Featured_2, etc.).

## Scheduling

The workflow schedule is configured with [cron syntax](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#schedule) to run every day at 8pm UTC when it looks like this: "0 20 * * *". We've modified it to run twice a day, once at 7AM and once at 11PM UTC. The five fields in the cron field refer to minute, hour, day of month, month, and day of week, respectively, making it super customizable. 

## Python Libraries

The main libraries used are:

- [`bs4`](https://www.crummy.com/software/BeautifulSoup/) - BeautifulSoup for parsing HTML
- [`requests`](https://requests.readthedocs.io/en/latest/) - Making HTTP requests to scrape web pages
- [`loguru`](https://github.com/Delgan/loguru) - Logging errors and run info
- [`pytz`](https://github.com/stub42/pytz) - Handling datetimes and timezones  
- [`waybackpy`](https://github.com/akamhy/waybackpy/) - Scraping web archives (optional)
