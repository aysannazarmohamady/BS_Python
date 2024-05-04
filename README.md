#  Beautiful Soup in Python for beginner learners

This repository is designed to help beginner learners understand and practice web scraping using the Beautiful Soup library in Python. It contains a series of Notebooks with explanations, examples, and exercises to guide you through the learning process.

## Table of Contents

1. [Introduction to Web Scraping](https://github.com/aysannazarmohamady/BS_Python/blob/main/README.md#1-introduction-to-web-scraping)
2. [Installing and Setting Up](https://github.com/aysannazarmohamady/BS_Python/blob/main/README.md#2-installing-and-setting-up)
3. [Beautiful Soup Basics](https://github.com/aysannazarmohamady/BS_Python/blob/main/README.md#3--beautiful-soup-basics)
4. [Extracting Data](https://github.com/aysannazarmohamady/BS_Python/blob/main/README.md#4-extracting-data)
5. [Advanced Topics](https://github.com/aysannazarmohamady/BS_Python/blob/main/README.md#5-advanced-topics)
6. [Projects and Exercises]()

## Getting Started

1. Clone the repository or download the ZIP file.
2. Install the required Python libraries (Beautiful Soup, requests, lxml).
3. Open the Jupyter *Notebooks/VS code/google colab* in the numbered order and follow along.
4. Complete the exercises and projects to reinforce your learning.

## Contributing

Contributions to this repository are welcome! If you find any issues or have suggestions for improvements, please open an issue or submit a pull request.


### 1. Introduction to Web Scraping

#### What is web scraping?
Web scraping is the process of extracting data from websites using software tools.

#### Use cases for web scraping
- Price monitoring and comparison
- Research and data analysis
- Job listing aggregation
- Content aggregation (news, articles, etc.)
- Lead generation and contact information extraction

#### Legal and ethical considerations
- nLegal and ethical considerations
- Check the website's terms of service and robots.txt file
- Respect the website's rate limiting and avoid overloading their servers
- Don't scrape sensitive or personal data without permission
- Give attribution and credit to the original source if required

  
### 2. Installing and Setting Up

- Installing Python
Install Python from the official website: https://www.python.org/downloads/

- Installing Beautiful Soup
```
import sys
!{sys.executable} -m pip install beautifulsoup4
```

- Installing other required libraries
```
!{sys.executable} -m pip install requests
!{sys.executable} -m pip install lxml
```
*This notebook guides you through installing Python, Beautiful Soup, and other required libraries (requests and lxml) on your system.*


### 3.  Beautiful Soup Basics

```
import requests
from bs4 import BeautifulSoup

# Fetching a webpage
url = "https://pythonprogramming.net/parsememcparseface/"
response = requests.get(url)
html_content = response.content

# Parsing the HTML
soup = BeautifulSoup(html_content, "html.parser")

# Navigating the parsed tree
print(soup.title)
# <title>Python Programming Tutorials</title>

print(soup.body.h1)


# Finding elements by tag
print(soup.find("h1"))


# Finding elements by attributes
print(soup.find("a", href="https://pythonprogramming.net/parsememcparseface/"))
# <a href="https://pythonprogramming.net/parsememcparseface/">More information...</a>
```


### 4. Extracting Data

```
import requests
from bs4 import BeautifulSoup

# Fetching a webpage
url = "https://pythonprogramming.net/parsememcparseface/"
response = requests.get(url)
html_content = response.content

# Parsing the HTML
soup = BeautifulSoup(html_content, "html.parser")

# Extracting text content
print(soup.body.p.text)
# This domain is for use in illustrative examples in documents.

# Extracting attributes
link = soup.find("a")
print(link["href"])


# Dealing with nested structures
for li in soup.ul.find_all("li"):
    print(li.text)
# List item 1
# List item 2
# List item 3
```

### 5. Advanced Topics

```
import requests
from bs4 import BeautifulSoup
import csv

# Handling JavaScript-rendered content
driver = webdriver.Chrome()
url = "https://www.example.com/dynamic-content"
driver.get(url)
html_content = driver.page_source
soup = BeautifulSoup(html_content, "html.parser")

# Working with CSV and Excel files
with open("data.csv", "w", newline="") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["Name", "Email", "Phone"])
    for contact in soup.find_all("div", class_="contact"):
        name = contact.find("h3").text
        email = contact.find("a").text
        phone = contact.find("span", class_="phone").text
        writer.writerow([name, email, phone])

# Scraping data from APIs
import requests
import json

api_url = "https://api.example.com/products"
response = requests.get(api_url)
data = json.loads(response.text)

for product in data["products"]:
    print(f"Name: {product['name']}, Price: {product['price']}")

# Handling pagination and crawling multiple pages
base_url = "https://www.example.com/products"
page = 1

while True:
    url = f"{base_url}?page={page}"
    response = requests.get(url)
    soup = BeautifulSoup(response.content, "html.parser")

    products = soup.find_all("div", class_="product")
    if not products:
        break

    for product in products:
        # Extract product data

    page += 1
    ```
