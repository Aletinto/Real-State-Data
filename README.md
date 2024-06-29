# Real-Estate-Data

Welcome all! This repository contains Python scripts for web scraping on atHome.

AtHome is one of the leading companies for real estate in Luxembourg. Having this data is extremely valuable, as there are no APIs or other ways to get the data.

## Project Overview
Easily collect detailed real estate data of Luxembourg.

## Key Features
- **User-Friendly**: Retrieve data even with minimal Python knowledge.
- **Comprehensive Data Gathering**: Automatically updates and records daily changes in listings.
- **Detailed Data**: Extracts price, description, rooms, bathrooms, garages, surface area, address, agency, images, and other characteristics.

## File Structure
The repository includes two main Jupyter notebooks:

### Notebooks
#### `get_all_links_athome.ipynb`
- **Purpose**: Collects all property listing links from athome.lu based on a search query on the regular web UI.
- **Functions**:
  - `get_latest_page(url_base: str)`: Determines the total number of pages for the search query.
  - `get_all_url(page_number: int, url_base: str)`: Fetches and filters URLs from a specified page.
  - `get_all_links(threads, url_base: str, last_page_number)`: Collects all links using multi-threading and structures them into a pandas DataFrame.
  - `main()`: Entry point to run the script and save all collected links to a pickle file.

#### `get_entity_details.ipynb`
- **Purpose**: Scrapes detailed information for each property from the collected links.
- **Functions**:
  - `clean_title(tag)`: Cleans and formats the property title.
  - `get_entity_details(link_url)`: Extracts property details from a given URL.
  - `build_dataframe(links)`: Constructs a DataFrame with all gathered property details using multi-threading.
  - `format_price_and_surface(result_df)`: Formats and processes price and surface area to handle intervals and absolute values.

## How to Use
1. **Get All Links**:
   - Execute `get_all_links_athome.ipynb`.
   - Specify the search query in `url_base`, you can do any kind of search, from rent to buy and different kinds of properties.
   - Run the script to save all property listing links to `list_of_links.pkl`.
2. **Get Property Details**:
   - Execute `get_entity_details.ipynb`.
   - Use the links obtained from the previous step.
   - Run the script to save detailed information in `raw_details_only_lux.csv`.

Other things

I have another implementation of the same code that runs on Native AWS Lambda and does this without manual execution. This code can also be implemented with multithreading. 

For small queries, this is good enough because it usually takes around 30 seconds for a regular search, but if the search becomes massive, multithreading or splitting this into partitions is the right way to go. However, this code is not public.

## Conclusion
We hope this tool simplifies your data collection process. Feel free to explore, modify the scripts for your specific needs, or contribute to the project.

Happy Scraping!