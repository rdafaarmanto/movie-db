# Movie DB

A movie search application built with React that fetches popular movies and search results from [The Movie Database (TMDB)](https://www.themoviedb.org/). It also tracks search counts in Appwrite and displays up to five of the most frequently searched movies.

## Features

- Displays popular movies from TMDB when the application loads.
- Searches for movies by title, with a one-second debounce after the last keystroke.
- Shows each movie's poster, rating, original language, and release year.
- Tracks search counts in Appwrite and displays the top movies by search frequency.
- Shows a loading indicator and an error message if fetching the movie list fails.

## Tech stack

- React 19 and Vite
- Tailwind CSS 4
- TMDB API
- Appwrite Databases

## Setup

Make sure Node.js and npm are installed. Create the required credentials and IDs in TMDB and Appwrite, then set up the environment file.

Add the following values to `.env.local`:

```dotenv
VITE_TMDB_API_KEY=your_tmdb_bearer_token
VITE_APPWRITE_PROJECT_ID=your_appwrite_project_id
VITE_APPWRITE_DATABASE_ID=your_appwrite_database_id
VITE_APPWRITE_COLLECTION_ID=your_appwrite_collection_id
```

`VITE_TMDB_API_KEY` is used to authenticate requests to TMDB. Create an Appwrite database and collection, and make sure the collection has these attributes:

| Attribute    | Type    | Purpose                            |
| ------------ | ------- | ---------------------------------- |
| `searchTerm` | String  | Movie search term                  |
| `count`      | Integer | Number of searches for the term    |
| `movie_id`   | Integer | ID of the corresponding TMDB movie |
| `poster_url` | String  | Movie poster URL                   |

Create indexes that support equality queries on `searchTerm` and descending order by `count`. Make sure the collection permissions allow the list, create, and update operations required by the application. The Appwrite endpoint is currently configured for the Singapore region in `src/appwrite.js`.

> **Security note:** Variables prefixed with `VITE_` are included in the frontend bundle and are visible to application users. Do not put server-side secrets in them. Use a TMDB token with appropriate access, and configure Appwrite permissions as narrowly as your use case allows.

## Run the application

Install dependencies and start the development server:

```sh
npm install
npm run dev
```

Vite prints the local URL in the terminal.

## Available scripts

```sh
npm run dev      # Start the development server
npm run build    # Create a production build in the dist/ directory
npm run preview  # Serve the production build locally
npm run lint     # Run ESLint
```
