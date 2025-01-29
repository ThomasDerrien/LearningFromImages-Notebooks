## Data Creation and Filtering

For this project, license plate images were scraped from the **PlatesMania website** using a custom-built scraper, which can be found on GitHub at [PlatesMania-Scraper](https://github.com/ThomasDerrien/PlatesMania-Scraper).

After collecting the data, we applied a filtering process to remove images from countries with special characters in their names, specifically: 
- URSS
- China
- Egypt
- Japan
- Mongolia
- Morocco
- Non Recognized
- Russia
- North Korea
- Thailand
- Saudi Arabia.

From the filtered dataset, we selected a total of **20,000 images**. These images were then split into three subsets for training, validation, and testing. 

The dataset was partitioned as follows:
- 70% for training,
- 15% for validation
- 15% for testing





