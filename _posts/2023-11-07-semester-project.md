---
layout: post
title:  "Golden Era Data Cleaning"
author: Tyler Smith
description: My project will analyze the Golden Era of Houston Astros baseball.
image: /assets/images/baseball.jpg
---

<h2>Introduction and Motivation</h2>

The Houston Astros have been to seven straight American League Championship Series and have played in the World Series four of the last seven years. This historic run of success
has resulted in two World Series Championships, causing Houston natives to deem this span of seven years as the "Golden Era" of Astros baseball. For my project, I will be diving
deep into the Golden Era of Astros baseball to analyze all sorts of different metrics during the last seven regular MLB seasons.

<h2>Data Collection and Cleaning</h2>

Sports analytics nerds like myself know that [Baseball Reference](https://www.baseball-reference.com/) is the place to go for baseball data. Before scraping the data, I made sure to check the robots.txt to ensure that I am safe to scrape the data. **Make sure to always check the robots.txt file before scraping a url!** Thanks for joining my data ethics lecture. 

Using the BeautifulSoup, requests, and pandas Python packages, I effectively created a dataframe of 1,032 rows and 20 columns containing Houston Astros regular season data between 2017-2023. I broke the websraping process into two steps to collect all the data that I wanted:

* Create a function to scrape regular season data
* Create a for loop that loops through a base url to quickly add season data a singular pandas dataframe

<h2>Webscraping Function</h2>

Here is a simplified walkthrough of the webscraping function:

**Define Function**
  * I defined my function as scrape_baseball_schedule(), which takes in a url parameter

```python
def scrape_baseball_schedule(url):
```

**Get HTML Content**
  * Using the requests package, I received the HTML content from the provided url
  * BeautifulSoup then joined the party to parse the content of the response provided by requests

```python
    response = requests.get(url)
    soup = BeautifulSoup(response.content, 'html.parser')
```

**Find the Table**
  * soup.find finds the element 'table' with the 'team_schedule' id

```python
    table = soup.find('table', id='team_schedule')
    rows = table.find_all('tr')
```

**Extract Column Headers**
 * Since the first row contains the column headers, a list comprehension is used to extract the text from each 'th' element

```python
header = [th.get_text(strip=True) for th in rows[0].find_all('th')]
```

**Extract Game Data**
 * Starting on the second row, the function then iterates over all rows in the table and extracts all 'th' and 'td' elements

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

**Create a Pandas Dataframe**
 * I use the 'games' list to create my dataframe
 * End the function by returning the dataframe

```python
        games.append(row_data)

    # Construct the DataFrame
    df = pd.DataFrame(games, columns=header)

    # Drop columns by index position
    df = df.drop(df.columns[[2, 21]], axis=1)
    
    return df
```

<h2>Loop to Clean Data</h2>

**Define a base URL and create an object for years**
 * Notice the curly brackets in the url. This for loop will start with 2023 and move back in time to collect the season data between 2017-2023

```python
base_url = 'https://www.baseball-reference.com/teams/HOU/{}-schedule-scores.shtml'

# Define the range of years you want to scrape
years = range(2023, 2023-7, -1)  # This will create a range from 2023 to 2017
```

**Loop over years**
 * Create a for loop to add each season to the base url
 * Use the scrape_baseball_reference() as defined above to scrape each season's url
 * Concatenate all season dataframes into one singular dataframe
 * Add a Season column to the concatenated dataframe for easy data manipulation during analysis

```python
# Loop over the years, scrape the data, and collect the DataFrames
season_dfs = []
for year in years:
    url = base_url.format(year)
    df = scrape_baseball_schedule(url)
    df['Season'] = year  # Add a column for the year/season
    season_dfs.append(df)
```

<h2>Conclusion</h2>

I hope that you were able to learn something about data collection and data cleansing from my post. For all of the data scientists in training, go explore different websites to find data that interests you and give webscraping a try. It is a valuable tool that will allow you to cater data analysis to your interests. Now that you have seen how I gathered seven seasons' worth of Houston Astros regular season baseball results, stay tuned for my exploratory data analysis so that we can dive deep into the Golden Era of Astros baseball. Feel free to check out my [GitHub Repository](https://github.com/tyler-c-smith04/semester_project) to see all of the code that I used to gather and clean my Astros data. Go 'Stros!

