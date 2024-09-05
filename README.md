# ReadMe - Movie Reviews and Data Integration from NYT and TMDB APIs

## Overview

This project retrieves movie reviews from the **New York Times API** and movie data from **The Movie Database (TMDB) API**. It filters for movie reviews with "love" in the headline, merges the data from both APIs, and exports the final dataset to a CSV file. The resulting dataset contains movie titles, release dates, genres, spoken languages, and production countries, alongside the NYT review data.

## Dependencies

The following Python libraries are required to run the script:

- `requests`: To make API calls.
- `dotenv`: To load environment variables (API keys).
- `pandas`: For data manipulation and analysis.
- `json`: For handling JSON data.
- `urllib.parse`: For encoding URL query parameters.

Install these dependencies using the command:

```bash
pip install requests python-dotenv pandas
```

## Setup

1. **API Keys**:  
   - Sign up for API access and get API keys from:
     - **New York Times Developer API** ([NYT Article Search API](https://developer.nytimes.com/docs/articlesearch-product/1/overview))
     - **TMDB API** ([TMDB API](https://www.themoviedb.org/documentation/api))
   
   - Add the following environment variables in a `.env` file in the root directory:
     ```bash
     NYT_API_KEY=your_nyt_api_key
     TMDB_API_KEY=your_tmdb_api_key
     ```

2. **Environment Setup**:
   - The script will load these keys from the `.env` file:
     ```python
     load_dotenv()
     nyt_api_key = os.getenv("NYT_API_KEY")
     tmdb_api_key = os.getenv("TMDB_API_KEY")
     ```

## Workflow

### 1. Retrieve NYT Movie Reviews
   - Fetches movie reviews that include "love" in the headline, from the "Movies" section of the **NYT Article Search API**.
   - The reviews are filtered for articles categorized as "Review" and are fetched within the date range `2013-01-01` to `2023-05-31`.
   - The data is retrieved in batches of 10 articles per request, looping through up to 20 pages.

### 2. Fetch Movie Details from TMDB
   - Based on the titles from the NYT reviews, the **TMDB API** is queried to fetch details for each movie, including:
     - Release date
     - Genres
     - Spoken languages
     - Production countries

### 3. Data Processing and Cleaning
   - The NYT and TMDB datasets are merged based on the movie titles.
   - Unnecessary columns are dropped, and data is formatted (e.g., genres, languages) to make it more readable.

### 4. Export Data to CSV
   - The cleaned, merged dataset is saved as `merged_movie_data.csv` without an index for further analysis or reporting.

## Running the Script

1. Ensure your `.env` file is correctly configured with the API keys.
2. Install the necessary dependencies:
   ```bash
   pip install requests python-dotenv pandas
   ```
3. Run the script:
   ```bash
   python script_name.py
   ```

## Sample Output

The resulting CSV file, `merged_movie_data.csv`, will contain the following columns:

- `web_url`: Link to the NYT review.
- `snippet`: Summary of the review.
- `source`: Source of the review (always "The New York Times").
- `pub_date`: Publication date of the review.
- `title`: Extracted movie title.
- `Release Date`: Release date from TMDB.
- `Genres`: Movie genres from TMDB.
- `Spoken Languages`: Languages spoken in the movie.
- `Production Countries`: Countries involved in the movie's production.

## Example Data Preview

Here is a preview of the first few rows of the merged dataset:

| web_url                                   | snippet                                                | title            | Release Date | Genres                   | Spoken Languages | Production Countries   |
|-------------------------------------------|--------------------------------------------------------|------------------|--------------|--------------------------|------------------|------------------------|
| https://www.nytimes.com/review1            | A beautiful tale of love and life.                     | Movie Title 1     | 2019-12-25   | Drama, Romance            | English          | United States          |
| https://www.nytimes.com/review2            | An action-packed love story set in the future.         | Movie Title 2     | 2018-06-15   | Action, Science Fiction   | English          | United Kingdom         |
| https://www.nytimes.com/review3            | A love story that transcends time and space.           | Movie Title 3     | 2021-03-10   | Adventure, Drama          | English          | United States, Canada  |

## License

This project is licensed under the MIT License. Feel free to use and modify it as needed.

--- 
