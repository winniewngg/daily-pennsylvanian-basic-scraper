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

The workflow schedule is configured with [cron syntax](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#schedule) to run:

- Every day at 8PM UTC

This once-daily scraping is a good rule-of-thumb, as it is generally respectful of the target website, as it does not contribute to any measurable burden to the site's resources.

You can use [crontab.guru](https://crontab.guru/) to generate your own cron schedule.

## Python Libraries

The main libraries used are:

- [`bs4`](https://www.crummy.com/software/BeautifulSoup/) - BeautifulSoup for parsing HTML
- [`requests`](https://requests.readthedocs.io/en/latest/) - Making HTTP requests to scrape web pages
- [`loguru`](https://github.com/Delgan/loguru) - Logging errors and run info
- [`pytz`](https://github.com/stub42/pytz) - Handling datetimes and timezones  
- [`waybackpy`](https://github.com/akamhy/waybackpy/) - Scraping web archives (optional)
