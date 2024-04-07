# Web-Scraping
## [1_requests](https://github.com/basu-binayak/Web-Scraping/tree/6db0564674245366ff1f2ee81ae9d1e15ef313bb/1_requests)
The requests module in Python is a powerful library used for making HTTP requests. It simplifies the process of sending HTTP requests and processing the responses. It's widely used for web scraping, interacting with RESTful APIs, and more.<br><br>
Here is an example usage:
```python
import requests

# Make a GET request to a website
response = requests.get('https://www.example.com')

# Check if the request was successful (status code 200)
if response.status_code == 200:
    # Print the content of the response
    print(response.text)
else:
    print('Error:', response.status_code)
```
This folder, **[1_requests](https://github.com/basu-binayak/Web-Scraping/tree/6db0564674245366ff1f2ee81ae9d1e15ef313bb/1_requests)** contains projects using just the **requests** module in Python.
