import openpyxl
import requests
from bs4 import BeautifulSoup

# Define the URL
url = 'https://store.steampowered.com/search/?filter=topsellers'

# Send a GET request to the URL
response = requests.get(url)

# Check if the request was successful
if response.status_code == 200:
    # Parse the page content
    soup = BeautifulSoup(response.content, 'html.parser')
    
    # Find game titles
    game_titles = soup.find_all('span', class_='title')
    
    # Find price containers
    price_containers = soup.find_all('div', class_='discount_final_price')
    
    # Find discount containers
    discount_containers = soup.find_all('div', class_='discount_pct')
    
    # Find release date containers
    release_dates = soup.find_all('div', class_='discount_block')
    
    # Loop through the titles and get other information
    for i, game in enumerate(game_titles):
        game_name = game.text.strip()
        
        # Get the price if available
        if i < len(price_containers):
            price = price_containers[i].text.strip()
        else:
            price = "Price not available"
        
        # Get the discount if available
        if i < len(discount_containers):
            discount = discount_containers[i].text.strip()
        else:
            discount = "No discount"
        
        # Get the release date if available
        if i < len(release_dates):
            release_date = release_dates[i].text.strip()
        else:
            release_date = "Release date not available"
        
        print(f"Game: {game_name} - Price: {price} - Discount: {discount} - Release Date: {release_date}")

    # Create a new Excel workbook
    workbook = openpyxl.Workbook()
    # Select the default sheet (usually named 'Sheet')
    sheet = workbook.active
    # Set the header row
    sheet.append(["Game", "Price", "Discount", "Release Date"])
    
    # Append game data to the Excel sheet
    for i, game in enumerate(game_titles):
        game_name = game.text.strip()
        
        if i < len(price_containers):
            price = price_containers[i].text.strip()
        else:
            price = "Price not available"
        
        if i < len(discount_containers):
            discount = discount_containers[i].text.strip()
        else:
            discount = "No discount"
        
        if i < len(release_dates):
            release_date = release_dates[i].text.strip()
        else:
            release_date = "Release date not available"
        
        sheet.append([game_name, price, discount, release_date])

    # Using raw string to avoid escape sequence issues
    save_path = r"C:\Users\Niklas\Documents\Python\Steam_Games.xlsx"

    # Save the workbook to the specified path
    workbook.save(save_path)
    print(f"Excel file created successfully at {save_path}")

else:
    print(f"Failed to retrieve data. Status code: {response.status_code}")
