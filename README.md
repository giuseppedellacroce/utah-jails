# Salt Lake County Jail Inmate Data Scraper

A Jupyter notebook-based web scraper that collects inmate information from the Salt Lake County Inmate Management System.

## Overview

This tool automates the collection of inmate data from the [Salt Lake County IML system](https://iml.saltlakecounty.gov/IML), gathering both basic roster information and detailed inmate records including demographics and charges.

## Features

- **Automated pagination**: Scrapes all pages of inmate search results
- **Detailed data collection**: Retrieves citizenship, country of birth, race, and charges for each inmate
- **Error recovery**: Handles failed lookups and allows for retry
- **Daily snapshots**: Saves data with date-stamped filenames for historical tracking

## Prerequisites

- Python 3.x
- Chrome browser
- ChromeDriver (must match your Chrome version)

## Installation

1. Clone or download this repository

2. Install required Python packages:
```bash
pip install selenium
```

3. Ensure ChromeDriver is installed and accessible in your PATH
   - Download from: https://chromedriver.chromium.org/
   - Or install via package manager (e.g., `brew install chromedriver` on macOS)

## Usage

Open `SL county jail.ipynb` in Jupyter Notebook or JupyterLab and run cells sequentially:

1. **Cell 0**: Install dependencies
2. **Cell 1**: Initialize browser and navigate to IML
3. **Cell 2**: Scrape all pages for basic inmate data
4. **Cell 3**: Save initial roster to CSV
5. **Cell 4**: Collect detailed information for each inmate
6. **Cell 5**: Retry any failed lookups
7. **Cell 6**: Save detailed data to CSV
8. **Cell 7**: Save skipped inmates list
9. **Cell 8**: Close browser

## Output Files

All data files are saved in the `data/` directory:

| File | Description |
|------|-------------|
| `inmate_data-{MM-DD-YYYY}.csv` | Daily snapshot of basic inmate roster (name, booking number) |
| `inmate_charges.csv` | Comprehensive data including citizenship, country of birth, race, and charges |
| `inmate_skipped.csv` | List of inmates that couldn't be processed (for manual review) |

## Data Fields

### Basic Data
- Name
- Booking number

### Detailed Data
- Name
- Booking number
- Citizenship
- Country of birth
- Race
- Charges (semicolon-separated list)

## Notes

- The scraper includes built-in delays (`time.sleep()`) to avoid overwhelming the server
- XPath selectors may break if the website structure changes
- The script navigates back to the main search page after errors to maintain stability
- Execution time depends on the number of inmates (typically several minutes)

## Legal and Ethical Considerations

This scraper accesses publicly available information from the Salt Lake County Inmate Management System. Users should:
- Respect the website's terms of service
- Use reasonable scraping intervals to avoid server overload
- Handle inmate data responsibly and in compliance with applicable privacy laws
- Be aware that inmate information is considered public record but should be used ethically

## Troubleshooting

**Browser doesn't open:**
- Verify ChromeDriver is installed and matches your Chrome version
- Check that ChromeDriver is in your system PATH

**XPath errors:**
- The website structure may have changed
- Inspect the current page HTML and update XPaths in the notebook

**Timeout errors:**
- Increase `time.sleep()` values or `WebDriverWait` timeout
- Check your internet connection

**Incomplete data:**
- Check `inmate_skipped.csv` for failed lookups
- Run Cell 5 to retry skipped inmates

## Contributing

This is a data collection tool. When modifying:
- Test thoroughly with a small dataset first
- Update XPaths if the website structure changes
- Maintain error handling to ensure graceful failures
- Document any new data fields or scraping logic
