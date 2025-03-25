# Web-scraping
Steam Top Sellers Scraper

## Overview

This Python script scrapes the Steam store's top-selling games, extracts their titles, prices, discounts, and release dates, and then saves the data to an Excel file.

## Features

Scrapes game titles, prices, discounts, and release dates from Steam's top sellers list.

Uses BeautifulSoup to parse HTML content.

Stores the extracted data in an Excel spreadsheet using OpenPyXL.

Handles cases where price, discount, or release date information may not be available.

## Requirements

Before running the script, ensure you have the following Python libraries installed:

pip install requests beautifulsoup4 openpyxl

How It Works

Sends a GET request to the Steam top sellers page.

Parses the HTML content using BeautifulSoup.

Extracts game data including:

Title

Price (if available)

Discount percentage (if available)

Release date (if available)

Prints the extracted data to the console.

Saves the data to an Excel file at C:\Users\Niklas\Documents\Python\Steam_Games.xlsx.

Usage

Run the script using Python:

python steam_scraper.py

After execution, an Excel file will be created with the scraped game data.

Output Example

The script prints the extracted game data in the following format:

Game: Counter-Strike 2 - Price: Free - Discount: -40% - Release Date: Free
Game: Farming Simulator 25 - Price: 49,99€ - Discount: -35% - Release Date: 49,99€
...
Excel file created successfully at C:\Users\Niklas\Documents\Python\Steam_Games.xlsx

Notes

If Steam changes its website structure, the script may need updates to locate the correct HTML elements.

Ensure your system has permission to write files to the specified Excel file path.

License

This project is open-source and available under the MIT License.
