## API Overview

The MoviesDatabase API provides a huge, constantly updated collection of information about movies, TV shows, and actors. It contains:

9+ million titles (movies, series, and episodes)

11+ million actors and crew members

Weekly updates for new titles

Daily updates for ratings and episodes

This API includes:

Ratings

Cast and crew

Trailers

Awards

Plot summaries

Photos and media

Episode guides

Biographies

Genres

And much more

It is ideal for apps that need movie data, search features, recommendations, or entertainment analytics.

## API Version

V1 (Current)

## Available Endpoints

🎬 Titles

Retrieve information about movies, TV shows, or episodes.

Endpoint Description

/titles Get multiple titles using optional filters (genre, year, type, etc.)

/x/titles-by-ids Fetch multiple titles using an array of IMDb IDs

/titles/{id} Get full details of a title using its IMDb ID

/titles/{id}/ratings Get rating and vote count for a title

/titles/series/{id} Get all episodes for a series (with episode number + season)

/titles/seasons/{id} Get number of seasons for a series

/titles/series/{id}/{season} Get all episodes in a specific season

/titles/episode/{id} Get full info about an individual episode

/titles/x/upcoming Get list of upcoming titles

🔍 Search Endpoints

Endpoint Description

/titles/search/keyword/{keyword} Search titles by keyword

/titles/search/title/{title} Search titles by name (exact or partial match)

/titles/search/akas/{aka} Search titles by alternate names (AKAs) — exact match only

🧑‍🎤 Actor Endpoints

Endpoint Description

/actors Get list of actors with pagination

/actors/{id} Get full biography and details of an actor

🛠 Utils

Endpoint Description

/title/utils/titleType Get all available title types (e.g., movie, series, short film)

/title/utils/genres Get all genres

/title/utils/lists Get predefined "lists" like Top
250, Most Popular, Box Office, etc.

📌 Optional Query Parameters

These parameters can be used on most endpoints:

Parameter Description

**info** STRING - Customize what fields to return (e.g. mini_info, image, rating, awards)

**limit** NUMBER - Number of items to return (max 50)
**page** NUMBER - Pagination page number
**titleType** STRING - Filter by title type (movie, series, etc.)
**startYear**/ **endYear** NUMBER - Filter by year range
**year** NUMBER - Filter by exact release year
**genre** STRING - Filter by genre (capitalized)
**sort** STRING - Sorting options (e.g., year.incr, year.decr)
**exact** STRING - Exact match for title searches
**list** STRING - Choose predefined lists like Top 250, Most Popular, etc.

## Request and Response Format

Example Request
GET /titles/tt1234567?info=base_info

Example Response
{
"results": {
"id": "tt1234567",
"titleText": { "text": "Ampomah" },
"releaseDate": { "year": 2025 },
"genres": ["Drama"],
"ratingsSummary": {
"averageRating": 8.2,
"numVotes": 12000
},
"plot": { "plotText": "The Rise of Andro." }
}
}

Response Format Always Includes:

results — Main data object or array

page — (if pagination is used)

next — URL for next page (if available)

entries — Count of returned items

## Authentication Requirements

The API uses RapidAPI headers for authentication.

Include these headers with every request:

{
"X-RapidAPI-Key": "YOUR_API_KEY",
"X-RapidAPI-Host": "moviesdatabase.p.rapidapi.com",
"Content-Type": "application/json"
}

## Error Handling

Error Code - Meaning - How to Fix

401 – Unauthorized API key missing/invalid Check your headers
404 – Not Found Invalid IMDb ID Verify the ID
429 – Too Many Requests Rate limit reached Slow down requests
500 – Server Error API backend issue Retry after some time
Recommended Error Handling in Code
try {
const res = await fetch(url, options);

if (!res.ok) {
throw new Error(`HTTP Error: ${res.status}`);
}

const data = await res.json();
} catch (err) {
console.error("API request failed:", err);
}

## Usage Limits & Best Practices

⏱️ Rate Limits

Depending on your plan on RapidAPI, usage may be limited per second/minute/day.

Best Practices

Use info=mini_info when you only need basic data.

Cache results to avoid extra API calls.

Always handle missing fields (not all movies have images or budget info).

Avoid fetching large lists at once — use pagination.

Validate user search input to prevent unnecessary requests.
