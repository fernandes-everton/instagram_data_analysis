# Instagram Data Analysis

This project is a data analysis pipeline developed on Google Colab. It performs the collection and analysis of Instagram profile and post data and classifies comments using the Google Gemini API.

## Table of Contents
- [Overview](#overview)
- [Environment Setup](#environment-setup)
- [Dependency Installation](#dependency-installation)
- [Usage](#usage)
- [Sensitive Variables](#sensitive-variables)
- [Technologies Used](#technologies-used)
- [Additional Notes](#additional-notes)

## Overview
This project involves the following steps:

1. **Environment Setup**: Installs and configures Apache Spark, Java and other libraries on Google Colab.
2. **Data Collection**: Retrieves Instagram profile, posts, and comments using the Instagram API.
3. **Comment Classification**: Uses the Google Gemini API to classify the sentiment of comments.
4. **Data Storage**: Stores the classified results in a DataLake for future analysis.
5. **Analysis and Processing**: Creates and saves DataFrames in Parquet format for analysis.

## Environment Setup
Before running the code, ensure that the environment is set up correctly. The project was developed on Google Colab and requires the installation of Apache Spark and Java. The code for setting up the environment is included in code cells within the Google Colab notebook.

## Dependency Installation
To install the necessary dependencies, execute the following cells in your Google Colab notebook:

   ```
   !pip install requests
   !apt-get update
   !apt-get install openjdk-8-jdk-headless -qq > /dev/null
   !wget -q http://archive.apache.org/dist/spark/spark-3.1.1/spark-3.1.1-bin-hadoop3.2.tgz
   !tar xf spark-3.1.1-bin-hadoop3.2.tgz
   !pip install pyspark==3.1.1
   !pip install -q findspark
   !pip install -U google-generativeai
   ```

## Usage
1. **Variable Setup**:  
   Ensure that you have the necessary API keys stored securely as Google Colab secrets. You will need:
      - `x-rapidapi-key`: For accessing the Instagram API.
      - `gemini_api_key`: For accessing the Google Gemini API.  
      
   These variables can be accessed using `userdata.get()` in Colab:

      ```python
      headers = {
         'x-rapidapi-key': userdata.get('x-rapidapi-key'),
         'x-rapidapi-host': 'instagram-scraper-api3.p.rapidapi.com'
      }

      gemini_api_key = userdata.get('gemini_api_key')
      ```

2. **Running the Code**:  
   The code is divided into sections that you can execute in Google Colab. Be sure to follow the order of the cells to ensure that all dependencies and variables are correctly configured.

   You can execute the main workflow using the following function:

   ```python
   # Replace with the correct values
   influencer = 'example_influencer'

   url = 'https://instagram-scraper-api3.p.rapidapi.com/'

   headers = {
	   'x-rapidapi-key': 'your_x-rapidapi-key',
	   'x-rapidapi-host': 'instagram-scraper-api3.p.rapidapi.com'
   }

   gemini_api_key = 'your_gemini_api_key'

   # Execute the workflow
   main(influencer, url, headers)
   classify_comments_for_the_latest_post(influencer, url, headers, gemini_api_key)
   ```

3. **Data Storage:**:  
   - Profiles, posts, and comments are saved in Parquet format in a specified directory on Google Drive.
   - The directory structure is partitioned by influencer and timestamp, allowing for efficient querying and future analysis.

## Sensitive Variables
The project requires two sensitive variables, which should be stored securely:
   - `x-rapidapi-key`: Used to access Instagram data.
   - `gemini_api_key`: Used to classify comments using the Google Gemini API.

These variables are retrieved from Google Colab's `userdata.get()` to avoid hardcoding them directly in the code.

## Technologies Used
This project leverages the following technologies:

   - **Google Colab**: Online development environment to run Jupyter notebooks in the cloud.
   - **Instagram API**: Data extraction from profiles and posts.
   - **Python**: A programming language used for scripting and data analysis.
   - **Requests**: A Python library for making HTTP requests.
   - **Apache Spark**: Handling and analyzing large volumes of data.
   - **PySpark**: A Python API for Apache Spark.
   - **Google Gemini API**: Sentiment classification with AI.
   - **Data Lake (Google Drive)**: Storing data for future analysis.

## Additional Notes
- This project was developed on Google Colab, taking advantage of the available infrastructure and resources for data processing and analysis.  
- Make sure to check and comply with the terms of service and usage limits of the APIs used.
