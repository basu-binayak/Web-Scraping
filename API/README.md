# How to interact with API?
> If you are new to API and have no knowledge, do refer to this awesome article on API in MEDIUM : <a href="https://medium.com/@basubinayak05/application-programming-interface-3c31ce6a4be3">Application Programming Interface(API)</a>

## Foreign Exchange Rate API
**Link : *https://www.exchangerate-api.com/***

- Get started by creating a free account. Once you create an account and verify your mail, you will get an API key which you can use to interact with this Exchange Rate API. 

**Link for the Documentation : *https://www.exchangerate-api.com/docs/overview***

**⚡ Fast Start**
- Use the Standard endpoint to get started right away. This returns a JSON object with exchange rates from your base currency to all our supported codes.


**⚙️ Main API**
- Standard : This is main API response format - given a supplied base currency it will return the whole list of other currencies we support and their corresponding exchange rates. (***https://www.exchangerate-api.com/docs/standard-requests***)

- Pair Conversion : Submit a pair of codes and optional amount in your request. You'll get back the exchange rate between the codes and the conversion of the optional amount if you included it. (***https://www.exchangerate-api.com/docs/pair-conversion-requests***)

Link for Python Guide : ***https://www.exchangerate-api.com/docs/python-currency-api***

- However, you can follow the <a href="https://github.com/basu-binayak/Web-Scraping/blob/b0e46143bdef342d6cc0193ad03e35f3077063f6/API/Exchange_Rate_API.ipynb">Exchange_Rate_API.ipynb</a> to get a better undertanding !


## BBC Weather Location Service 
> Note: Here we will use the `Network` tab of the developers tab to get to the API. 

### Identify the API Call made by the Service 
![Understanding the API Call](https://example.com/weather-icon.png)

To identify the API call made by a website like BBC Weather when you search for a location (such as "Singapore"), you can follow these steps using the Developer Tools in your browser (Chrome or Firefox):

#### Steps to Identify the API in the Network Tab
**Open the Developer Tools**
- Right-click anywhere on the BBC Weather page and select Inspect or press Ctrl + Shift + I (Windows/Linux) or Cmd + Option + I (Mac).
- Navigate to the Network tab.

**Clear any existing logs**
- To avoid confusion with previous network requests, click the clear button (often represented by a circle with a line or an "X" icon) to clear existing logs.

**Search for, say , 'Singapore' on the BBC Weather site**
- In the search bar on the BBC Weather page, type "Singapore" and hit Enter.
- The page will reload with weather data for Singapore, and you’ll notice several network requests being made.

**Filter to API requests**
- In the Network tab, look for the XHR (XMLHttpRequest) filter or select "Fetch/XHR". This filter will show requests made by the site that return data in formats like JSON or XML (typically used in API calls).
- You can also use the All tab to view all requests, but focusing on XHR narrows it down to API-related calls.

**Find the API Request**
- Look for a request that seems to fetch data related to your search. The URL often contains keywords like weather, forecast, location, or Singapore or some code 
- The Method column will typically show GET or POST for API requests. The request might look something like: https://api.bbc.com/weather/.../singapore.

**Inspect the Request**
- Click on the request that looks relevant. In the Headers tab, you can see the full URL of the API request.
- In the Response tab, you will see the data that the API returns (usually in JSON format). This is the actual weather data for Singapore.

**Copy the API URL**
- Once you find the correct request, you can copy the API URL and use it in your own script or tool to fetch the weather data.







