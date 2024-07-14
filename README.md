# Web Scraper and Regular Expression Project

## Background

This project is a Python practice exercise that offered by [Analyst Builder](https://www.analystbuilder.com/) aimed at demonstrating skills in web scraping, data cleaning, and data analysis. The primary objective is to extract and process text data from a webpage and analyze the frequency of words used in the text.

## Purpose

The purpose of this project is to:

1. Practice web scraping techniques using BeautifulSoup.
2. Apply regular expressions for text processing.
3. Perform data cleaning and analysis to extract meaningful insights.
4. Demonstrate proficiency in Python for data extraction, cleaning, and analysis.

## Problem Statement

The goal is to scrape the text of Martin Luther King Jr.'s famous "I Have a Dream" speech from a webpage, clean the text by removing unnecessary characters and formatting, and analyze the frequency of words used in the speech. This analysis can help understand the emphasis and key themes of the speech.

## Files in this Repository
- [Python Script for Web Scraper + Regular Expression Project](https://github.com/ttfwang/web_scraper-regular_expression_project/blob/main/Web%20Scraper%20%2B%20Regular%20Expression%20Project.ipynb)

## Process

### 1. Import Libraries
  ```
  from bs4 import BeautifulSoup
  import requests
  import re
  import pandas as pd
  ```

### 2. Web Scraping

1. This step involves making an HTTP request to fetch the webpage content.
   ```
   url = "http://analytictech.com/mb021/mlk.htm"
   page = requests.get(url)
   soup = BeautifulSoup(page.text, "html.parser")
   print(soup)
   ```
2. Extract all paragraph tags from the HTML content.
   ```
   mlkj_speech = soup.find_all("p")
   ```
3. Combine the text from all paragraph tags into a single string.
   ```
   speech_combined = [p.text for p in mlkj_speech]
   string_speech = ''.join(speech_combined)
   ```

### 3. Text Cleaning and Processing

1. Replace line break characters with a space to clean up the text.
   ```
   string_speech_cleaned = string_speech.replace("\r\n", " ")
   print(string_speech_cleaned)
   ```

2. Use a regular expression to remove all punctuation from the text.
   ```
   speech_no_punt = re.sub(r"[^\w\s]", "", string_speech_cleaned)
   print(speech_no_punt)
   ```
3. Convert the text to lowercase to ensure uniformity.
   ```
   speech_lower = speech_no_punt.lower()
   print(speech_lower)
   ```
4. Split the cleaned text into individual words.
   ```
   speech_broken_out = re.split(r"\s+", speech_lower)
   ```
### 4. Data Analysis

1. Create a DataFrame and count the frequency of each word.
   ```
   df = pd.DataFrame(speech_broken_out, columns=['Word']).value_counts().reset_index(name='Count')
   print(df)
   ```
   
2. Save the word frequency counts to a CSV file.
   ```
   df.to_csv(r"C:\Users\tengf\OneDrive\Documents\Document_Tengfei Wang\Personal learning document\Python learning\MLKJ_Speech_Counts.csv",    index_label='Word')
   ```

## Findings

  - The word frequencies highlight the emphasis on key themes such as freedom, justice, and equality.
  - Commonly used words include "the," "of," "to," "and," and "a," which are typical in most English texts, but key thematic words like "freedom" and "dream" also appear frequently.

## Areas for Improvement
- Further analysis could involve removing stopwords to focus on more meaningful words.
- Visualizing the word frequencies using a bar chart or word cloud could provide better insights.
- Expanding the web scraping to other speeches or documents for comparative analysis.

## Conclusion

This project showcases my ability to use web scraping and regular expressions to extract and process data. By completing this project, I have reinforced my understanding of data extraction, text processing, and data cleaning techniques in Python.
