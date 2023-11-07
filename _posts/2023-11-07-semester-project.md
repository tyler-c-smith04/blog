---
layout: post
title:  "386 Semester Project"
author: Tyler Smith
description: My project will analyze the Golden Era of Houston Astros baseball.
image:
---

<h2>Introduction and Motivation</h2>

The Houston Astros have been to seven straight American League Championship Series and have played in the World Series four of the last seven years. This historic run of success
has resulted in two World Series Championships, causing Houston natives to deem this span of seven years as the "Golden Era" of Astros baseball. For my project, I will be diving
deep into the Golden Era of Astros baseball to analyze all sorts of different metrics during the last seven regular MLB seasons.

<h2>Data Collection and Cleaning</h2>

Sports analytics nerds like myself know that [Baseball Reference](https://www.baseball-reference.com/) is the place to go for baseball data. Using the BeautifulSoup, requests, and pandas Python packages, I effectively created a dataframe of 1,032 rows and 20 columns containing Houston Astros regular season data between 2017-2023. I broke the websraping process into two steps to collect all the data that I wanted:

* Create a function to scrape regular season data
* Create a for loop that loops through a base url to quickly add season data a singular pandas dataframe

<h2>Webscraping Function</h2>

Here is a simplified walkthrough of the webscraping function

Define Function
  * I defined my function as scrape_baseball_schedule(), which takes in a url parameter.

```python
def scrape_baseball_schedule(url):
```

Get HTML Content
  * Using the requests package, I received the HTML content from the provided url.
  * BeautifulSoup then joined the party to parse the content of the response provided by requests.

```python
    response = requests.get(url)
    soup = BeautifulSoup(response.content, 'html.parser')
```

Find the Table
  * soup.find finds the element 'table' with the 'team_schedule' id.

```python
    table = soup.find('table', id='team_schedule')
    rows = table.find_all('tr')
```

Extract Column Headers
 * Since the first row contains the column headers, a list comprehension is used to extract the text from each 'th' element.

```python
header = [th.get_text(strip=True) for th in rows[0].find_all('th')]
```

Extract Game Data
 * Starting on the second row, the function then iterates over all rows in the table and extracts all 'th' and 'td' elements.

```python
    games = []
    for row in rows[1:]:
        row_data = [cell.get_text(strip=True) for cell in row.find_all(['td', 'th'])]  # Get both td and th cells
        
        # Check if the first cell in the row_data is numeric
        # If not, we skip adding this row to our data
        if not row_data[0].isdigit():
            continue
        
        if len(row_data) != len(header):  # Check for discrepancies
            print(f"Row discrepancy: Expected {len(header)} columns but got {len(rowData)}.")
            row_data.extend([''] * (len(header) - len(row_data)))  # Add empty strings for missing columns
```

Create a Pandas Dataframe
 * I use the 'games' list to create my dataframe.
 * End the function by returning the dataframe.

```python
        games.append(row_data)

    # Construct the DataFrame
    df = pd.DataFrame(games, columns=header)

    # Drop columns by index position
    df = df.drop(df.columns[[2, 21]], axis=1)
    
    return df
```


