# Web Scraping using Google Sheets

## Whar are we scraping?
I am going to scrape a wikipedia page (https://en.wikipedia.org/wiki/Indian_Premier_League) which containes details of the IPL (Indian Premier League). I want a particular table from the entire page. I am using Google Sheets to perform this operation. 

## Step by Step guide 
**Step 1: Open Google Sheets**
- Open your web browser and go to Google Sheets.
- Create a new blank spreadsheet.

**Step 2: Use the IMPORTHTML Function**
- In the first cell where you want to import the data (e.g., A1), type the following:  `=IMPORTHTML("https://www.timeanddate.com/weather/india/kolkata/ext", "table", 1)`
> - URL: "https://en.wikipedia.org/wiki/Indian_Premier_League" is the webpage containing the data you want to scrape.
> - Query Type: "table" tells Google Sheets that you want to extract data from a table on the webpage.
> - Index: 1 specifies the first table on the webpage. If the data you want is in a different table, adjust the index (e.g., 2, 3).

- In our example, the table that we want is the number 10 in the webpage. How do I know this? You can watch the video below!
[![Watch the video](https://github.com/basu-binayak/Web-Scraping/blob/a9786d8b49a66a19bb71efd90fa5d8594ef7e8b9/Google%20Sheets%20Web%20Scraping/images/thumbnail.png)](https://github.com/basu-binayak/Web-Scraping/blob/a9786d8b49a66a19bb71efd90fa5d8594ef7e8b9/Google%20Sheets%20Web%20Scraping/videos/Table_number.mp4)
>> **Step 1: Open Developer Tools**
>>> - Open the webpage in a browser (e.g., Chrome, Firefox).
>>> - Right-click anywhere on the webpage and select Inspect or press Ctrl + Shift + I (Windows) or Cmd + Option + I (Mac) to open the Developer Tools.

>> **Step 2: Inspect the HTML Structure**
>>> - In the Elements tab of Developer Tools, you'll see the HTML code of the page.
Hover your mouse over the elements in the HTML code, and the corresponding elements will be highlighted on the webpage.

>> **Step 3: Locate the Tables**
>>> - Use the search functionality in Developer Tools. Press Ctrl + F (Windows) or Cmd + F (Mac) and type \<table\> to search for all \<table\> elements.
>>> - The search will highlight all the \<table\> tags. Use the up and down arrows to navigate between them.

>> **Step 4: Identify the Correct Table**
>>> - As you navigate through the \<table\> elements, the corresponding table on the webpage will be highlighted.
>>> - Check the content of each highlighted table to find the one you're looking for. If it’s the first table, it will be table 1; if it’s the second, it will be table 2, and so on.
>>> - Count the \<table\> tags from the top of the HTML document to determine the index number of the table you need.


**Step 3: Wait for Data to Load**
- After you enter the formula, Google Sheets will take a few moments to fetch and display the data from the webpage.

**Step 4: Clean Up the Data (Optional)**
- The data will likely include some unnecessary rows or columns. Use standard Google Sheets features to clean and format the data:
- Delete Unnecessary Rows/Columns: Highlight and delete rows/columns that contain unwanted data.
- Split Data: Use Data > Split Text to Columns to split any combined data (e.g., date and time) into separate columns.

**Step 5: Use ARRAYFORMULA (Optional for Dynamic Formatting)**
- If you need to apply formulas to a range of cells dynamically, you can use the ARRAYFORMULA function to manipulate data in bulk.

**Step 6: Refresh the Data Automatically**
- Google Sheets will automatically refresh the data periodically. However, if you want to refresh the data manually, you can re-enter the IMPORTHTML function or simply reload the spreadsheet.

**Step 7: Save and Share**
- Once the data is properly scraped and formatted, save your Google Sheet.
You can share the sheet with others by using the Share button in the top-right corner and specifying access permissions.

## Sharing the data scraped 
Link : 

> Notes:
- Limitations: Google Sheets can have limitations on the size of the data it can scrape at once. If the dataset is large, it might not import all data or could run into issues.
- Error Handling: If Google Sheets encounters any issue with the website (e.g., the table is not recognized), it will show an error. Try adjusting the table index in the IMPORTHTML function, or inspect the website structure using the browser's developer tools to find the correct table.
