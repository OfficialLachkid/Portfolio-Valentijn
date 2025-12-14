<div style="display: flex; gap: 50px;">
  <img src="Images/Experiments/Website_Scraper.gif" style="width: 40%;" />
  <img src="Images/Experiments/Scraped_Products_Zakkenspecialist.png" style="width: 50%;" />
</div>

[.CSV File Link](https://docs.google.com/spreadsheets/d/14K_JwxFZZVmEcMlxrLMKSTLnv4UAjcfedXByzlQtX7Y/edit?usp=sharing)

# Website Scraper

This document describes the process I followed to design and realise an automated product‑scraping system. The goal of this system is to efficiently extract product information from websites and store it in .csv format. This allows external systems to access product data efficiently, such as chatbots.


## Objective

I wanted to build a solution that can automatically collect product data from a website without requiring manual copying, since this can be very time consuming.

The scraper gathers the product title, description, product URL, and image URL, and stores this information in a CSV file. This CSV file can then be used as an input source for any system that depends on accurate and up‑to‑date product metadata. Set of retrieve data can be expended to more elements, such as product color for instance.


## Realise the Scraper

I began by analysing the structure of the website. Product pages often vary in layout/code, so it was important to inspect the HTML, identify patterns, and determine where key information such as product names and images was located. Scraping was designed for a single website, however, the code structure can simply be rewritten to fit another website's structure.

After mapping the website’s structure, I built the initial version of the scraper using Selenium. It could load product cards, extract basic information, and export the results to a CSV file. I refined the scraper over several iterations, improving reliability and flexibility as much as I could.

I implemented logic to detect and interact with a “load more” button. Many modern websites load additional items dynamically, so the scraper needed to repeat this action until all products were visible.

The system was then expanded to visit every product detail page. These pages typically contain more in-depth descriptions and higher‑quality images than the overview pages. I designed the scraper to merge the overview data with the more complete detail page data.

Finally, I added support for discovering additional products through “related items” links. These are often hidden inside detail pages and not visible from the main product listing. By following these links, the scraper builds a more complete dataset. In addition, this approach was noticeable faster than scraping from the overview page.


## Scraper Workflow

The scraper works in four structured phases:

### Phase 1: Loading the Overview Page
The script launches a Chrome browser using **Selenium**. It loads the base URL and checks whether additional products can be loaded. If a “load more” button is available, the scraper clicks it and waits until new products appear, repeating this step as needed.

### Phase 2: Scraping Overview Product Cards
Each visible product card is scanned for:
- Title  
- Short description  
- Link to the product detail page  
- Product image  

### Phase 3: Scraping Product Detail Pages
For each found product link, the scraper:
- Opens the detail page  
- Extracts the full product name  
- Finds a detailed description  
- Retrieves the main product image  
- Detects any `"meer/more details"` links linking to related products  

If new product links are discovered, they are added to a queue and processed until all unique items are scraped.

The scraper uses multiple fallback strategies for locating text and images. However, if a website differs to much structure-wise, then the code has to be slightly adjusted.

### Phase 4: Exporting the Result
All final records are written into a CSV file. This format opens cleanly inside database environments

Each row contains:
- product_name  
- product_description  
- product_link  
- product_image  


## Summary

This system handles the process of collecting product information from a website. It scans the product overview, follows all available product links, follows related product links, extracts detailed information, and stores the results in a structured CSV file.   
By combining dynamic page handling, fallback extraction logic, and link discovery, the scraper reduces manual work and enables rapid integration with external systems wherever needed.  
The script can be easily adjusted to fit different structured websites.

