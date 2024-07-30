# Moviesaya Documentation

Welcome to the **Moviesaya** documentation! This guide provides comprehensive instructions on setting up and using the Moviesaya app, which leverages The Movie Database (TMDb) API to provide users with information about popular movies, top-rated movies, and IMDB ratings.

## Table of Contents

1. [Introduction](#introduction)
2. [Features](#features)
3. [Prerequisites](#prerequisites)
4. [Installation and Setup](#installation-and-setup)
5. [Project Structure](#project-structure)
6. [API Integration](#api-integration)
7. [Key Components](#key-components)
8. [Navigation](#navigation)
9. [Error Handling](#error-handling)
10. [Troubleshooting](#troubleshooting)
11. [Contributing](#contributing)
12. [License](#license)

---

## Introduction

**Moviesaya** is a cross-platform mobile application built with React Native, providing users with information about movies including popular titles, top-rated selections, and IMDB ratings. By integrating with The Movie Database (TMDb) API, Moviesaya offers a rich collection of movie data with a smooth and responsive user interface.

## Features

- **Popular Movies**: Browse a list of trending movies worldwide.
- **Top Rated Movies**: Discover movies that have received high ratings.
- **Movie Details**: View detailed information about each movie, including synopsis, release date, and IMDB rating.
- **Search Functionality**: Find movies by title, genre, or other criteria.
- **Responsive Design**: Enjoy a seamless experience on both Android and iOS devices.

## Prerequisites

Before setting up Moviesaya, ensure you have the following tools and requirements:

- [Node.js](https://nodejs.org/) (v14 or higher)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- [React Native CLI](https://reactnative.dev/docs/environment-setup) or [Expo CLI](https://docs.expo.dev/get-started/installation/)
- [Android Studio](https://developer.android.com/studio) and/or [Xcode](https://developer.apple.com/xcode/) (for iOS development)
- A TMDb API key (register at [TMDb](https://www.themoviedb.org/documentation/api))

## Installation and Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/kymrhys2k22/moviesaya.git
cd moviesaya
```

### Step 2: Install Dependencies

Using npm:

```bash
npm install
```

Or using yarn:

```bash
yarn install
```

### Step 3: Configure Environment Variables

Create a `.env` file in the root directory and add your TMDb API key:

```plaintext
TMDB_API_KEY=your_api_key_here
```

### Step 4: Start the Development Server

#### Using React Native CLI:

For Android:

```bash
npx react-native run-android
```

For iOS:

```bash
npx react-native run-ios
```

#### Using Expo CLI:

```bash
expo start
```

Scan the QR code with your Expo Go app or use an emulator to view the app.

## Project Structure

The following is an overview of the Moviesaya project structure:

```plaintext
Moviesaya/
├── android/
├── ios/
├── src/
│   ├── components/
│   │   ├── MovieCard.js
│   │   ├── MovieList.js
│   │   ├── MovieDetail.js
│   │   └── SearchBar.js
│   ├── screens/
│   │   ├── HomeScreen.js
│   │   ├── TopRatedScreen.js
│   │   ├── MovieDetailScreen.js
│   │   └── SearchScreen.js
│   ├── navigation/
│   │   └── AppNavigator.js
│   ├── utils/
│   │   └── api.js
│   ├── assets/
│   ├── styles/
│   │   └── styles.js
│   ├── App.js
│   └── config.js
├── .env
├── package.json
└── README.md
```

### Key Directories and Files

- **`src/components`**: Reusable UI components like `MovieCard`, `MovieList`, etc.
- **`src/screens`**: Screen components that represent different app pages.
- **`src/navigation`**: Navigation setup and configuration using React Navigation.
- **`src/utils`**: Utility functions, including API calls.
- **`src/styles`**: Stylesheets for consistent styling across components.
- **`config.js`**: Configuration file for managing API keys and base URLs.
- **`.env`**: Environment variables, including the TMDb API key.

## API Integration

The Movie Database (TMDb) API provides access to a wealth of movie data. Below are the primary API endpoints used in Moviesaya:

### Base URL

```plaintext
https://api.themoviedb.org/3/
```

### 1. Popular Movies

**Endpoint:** `GET /movie/popular`

**Description:** Retrieve a list of popular movies.

**Example Request:**

```javascript
const fetchPopularMovies = async () => {
  try {
    const response = await fetch(`https://api.themoviedb.org/3/movie/popular?api_key=${process.env.TMDB_API_KEY}&language=en-US&page=1`);
    const data = await response.json();
    return data.results;
  } catch (error) {
    console.error('Error fetching popular movies:', error);
  }
};
```

### 2. Top Rated Movies

**Endpoint:** `GET /movie/top_rated`

**Description:** Fetch a list of top-rated movies.

**Example Request:**

```javascript
const fetchTopRatedMovies = async () => {
  try {
    const response = await fetch(`https://api.themoviedb.org/3/movie/top_rated?api_key=${process.env.TMDB_API_KEY}&language=en-US&page=1`);
    const data = await response.json();
    return data.results;
  } catch (error) {
    console.error('Error fetching top-rated movies:', error);
  }
};
```

### 3. Movie Details (Including IMDB Rating)

**Endpoint:** `GET /movie/{movie_id}`

**Description:** Fetch detailed information about a specific movie.

**Example Request:**

```javascript
const fetchMovieDetails = async (movieId) => {
  try {
    const response = await fetch(`https://api.themoviedb.org/3/movie/${movieId}?api_key=${process.env.TMDB_API_KEY}&language=en-US`);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error fetching movie details:', error);
  }
};
```

## Key Components

### 1. MovieCard

Displays individual movie information in a card format.

**File:** `src/components/MovieCard.js`

**Props:**

- `movie` (object): Movie data object containing title, poster, rating, etc.
- `onPress` (function): Function to handle card press events.

**Example Usage:**

```javascript
<MovieCard
  movie={movie}
  onPress={() => navigateToDetail(movie.id)}
/>
```

### 2. MovieList

Renders a list of movies using `FlatList`.

**File:** `src/components/MovieList.js`

**Props:**

- `movies` (array): Array of movie objects.
- `onMovieSelect` (function): Function to handle movie selection.

**Example Usage:**

```javascript
<MovieList
  movies={popularMovies}
  onMovieSelect={navigateToDetail}
/>
```

### 3. MovieDetail

Displays detailed information about a selected movie.

**File:** `src/components/MovieDetail.js`

**Props:**

- `movie` (object): Movie data object with details to display.

**Example Usage:**

```javascript
<MovieDetail movie={selectedMovie} />
```

### 4. SearchBar

Provides a search input for finding movies by title.

**File:** `src/components/SearchBar.js`

**Props:**

- `onSearch` (function): Function to handle search input.

**Example Usage:**

```javascript
<SearchBar onSearch={handleSearch} />
```

## Navigation

Moviesaya uses [React Navigation](https://reactnavigation.org/) for handling app navigation.

### AppNavigator

Defines the main navigation structure of the app.

**File:** `src/navigation/AppNavigator.js`

**Configuration:**

```javascript
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';

import HomeScreen from '../screens/HomeScreen';
import TopRatedScreen from '../screens/TopRatedScreen';
import MovieDetailScreen from '../screens/MovieDetailScreen';

const Stack = createStackNavigator();

const AppNavigator = () => (
  <NavigationContainer>
    <Stack.Navigator initialRouteName="Home">
      <Stack.Screen name="Home" component={HomeScreen} />
      <Stack.Screen name="TopRated" component={TopRatedScreen} />
      <Stack.Screen name="MovieDetail" component={MovieDetail
