# How to Use ChatGPT for Web Scraping in 2024

[![Oxylabs promo code](https://raw.githubusercontent.com/oxylabs/product-integrations/refs/heads/master/Affiliate-Universal-1090x275.png)](https://oxylabs.go2cloud.org/aff_c?offer_id=7&aff_id=877&url_id=112)

[![](https://dcbadge.vercel.app/api/server/eWsVUJrnG5)](https://discord.gg/Pds3gBmKMH)

 * [Locate the elements to scrape](#locate-the-elements-to-scrape)
  * [Prepare the ChatGPT prompt](#prepare-the-chatgpt-prompt)
  * [Review the code](#review-the-code)
  * [Execute and test](#execute-and-test)
    + [Code Editing Assistance](#code-editing-assistance)
    + [Code Linting](#code-linting)
    + [Code Optimization](#code-optimization)
    + [Handling Dynamic Content](#handling-dynamic-content)
  * [Conclusion](#conclusion)

In this tutorial, we'll demonstrate how to extract data with ChatGPT from [Oxylabs Sandbox](https://sandbox.oxylabs.io/products), a dummy e-commerce store that maintains video game listings in several categories. 

## Locate the elements to scrape 

Before prompting ChatGPT, let’s first locate the elements we need to extract from the target page. Assume that we need only the video game titles and prices. First, right-click one of the game titles and select “Inspect.” This will open the HTML code for this element in the Developer Tools window.

Then, right-click the element and select “Copy selector” with the game title in it. The following figure explains it all. Write down the selector and repeat the same to find the selector for the Price element. 

## Prepare the ChatGPT prompt 

The prompt should be well-explained, specifying the code’s programming language, tools and libraries to be used, element selectors, output, and any special instructions the code must comply with. Here is a sample prompt that you can use to create the web scraper using Python and & BeautifulSoup:

```
Write a web scraper using Python and BeautifulSoup.


Sample Target: https://sandbox.oxylabs.io/products 

Rationale: Scrape the video game titles and prices of all the games on the target page.


CSS selectors are as follows:

1. Title: #__next > main > div > div > div > div:nth-child(2) > div > div:nth-child(1) > a.card-header.css-o171kl.eag3qlw2 > h4

2. Price: #__next > main > div > div > div > div:nth-child(2) > div > div:nth-child(1) > div.price-wrapper.css-li4v8k.eag3qlw4


Output: Save all the Titles and Prices for all the video games in a CSV file


Additional Instructions: Handle character encoding and remove undesirable symbols in the output CSV.
```

Notice we have provided CSS selectors for prices and titles that we copied in the earlier step. 

The scraped data might contain a few odd characters if not handled properly due to encoding issues. It happens when the web page and the Python script interpret the character encoding differently. Therefore, we can add relevant Additional Instructions to avoid these encoding issues. 

## Review the code

Once ChatGPT replies with a code, it’s always a good idea to review it first. Just overview the code if it seems to do what you want it to do. Double-check if it uses some libraries or packages you may wish to exclude. If you find any inherent glitches, write back to ChatGPT and ask to generate the code again.

## Execute and test 

Copy the ChatGPT-generated code and check if it is executing fine. Here is the code that ChatGPT generated for us:

```
import requests
from bs4 import BeautifulSoup
import csv

# URL of the target page
url = "https://sandbox.oxylabs.io/products"

# Send a GET request to the URL
response = requests.get(url)

# Parse the HTML content using BeautifulSoup
soup = BeautifulSoup(response.content, "html.parser")

# CSS selectors for title and price
title_selector = "a.card-header h4"
price_selector = "div.price-wrapper"

# Find all game titles and prices
titles = soup.select(title_selector)
prices = soup.select(price_selector)

# Create a list to store the data
data = []

# Iterate through the titles and prices
for title, price in zip(titles, prices):
    game_title = title.get_text(strip=True)
    game_price = price.get_text(strip=True)
    data.append((game_title, game_price))

# Define the CSV filename
filename = "game_data.csv"

# Write the data to a CSV file
with open(filename, "w", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)
    writer.writerow(["Title", "Price"])  # Write header
    for game in data:
        writer.writerow(game)

print(f"Data scraped successfully and saved to '{filename}'.")
```

Note: Remember to install the `BeautifulSoup` library and  `requests` library before running the code. This can be done by opening the terminal and running:

```
pip install requests beautifulsoup4
```

That's it–we've successfully scraped our target website. However, there are also certain tips and tricks that you can follow to get the most accurate and desired information from ChatGPT: 

### Code Editing Assistance
ChatGPT can refine and adjust code based on your needs. Specify changes like modifying scraped elements, improving code effectiveness, or altering data extraction processes. It can generate alternatives or suggest improvements for web scraping tasks.

### Code Linting
Improve code readability and maintainability by asking ChatGPT to lint your code. Paste your code and request best practices, syntax fixes, or readability enhancements by including "lint the code" in your prompt.

### Code Optimization
For efficient web scraping, especially with large datasets, ChatGPT can suggest optimizations like using faster frameworks, caching, parallel processing, or reducing unnecessary network calls.

### Handling Dynamic Content
For websites with dynamic or JavaScript-rendered content, ChatGPT can guide you in using headlfess browsers, parsing dynamic HTML, or automating user interactions to access complex web content.

## Conclusion 

For your convenience, we also have this tutorial available in [blog post](https://oxylabs.io/blog/chatgpt-web-scraping) and [video](https://www.youtube.com/watch?v=AUEjBzLJlE4) formats. 

 
