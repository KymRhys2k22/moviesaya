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


---

## Navigation (continued)

### AppNavigator (continued)

**File:** `src/navigation/AppNavigator.js`

**Configuration:**

```javascript
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';

import HomeScreen from '../screens/HomeScreen';
import TopRatedScreen from '../screens/TopRatedScreen';
import MovieDetailScreen from '../screens/MovieDetailScreen';
import SearchScreen from '../screens/SearchScreen';

const Stack = createStackNavigator();

const AppNavigator = () => (
  <NavigationContainer>
    <Stack.Navigator initialRouteName="Home">
      <Stack.Screen 
        name="Home" 
        component={HomeScreen} 
        options={{ title: 'Moviesaya' }}
      />
      <Stack.Screen 
        name="TopRated" 
        component={TopRatedScreen} 
        options={{ title: 'Top Rated Movies' }}
      />
      <Stack.Screen 
        name="MovieDetail" 
        component={MovieDetailScreen} 
        options={({ route }) => ({ title: route.params.movieTitle })}
      />
      <Stack.Screen 
        name="Search" 
        component={SearchScreen} 
        options={{ title: 'Search Movies' }}
      />
    </Stack.Navigator>
  </NavigationContainer>
);

export default AppNavigator;
```

### Screens Description

1. **HomeScreen**
   - Displays a list of popular movies.
   - Allows navigation to `MovieDetailScreen` for detailed movie information.

2. **TopRatedScreen**
   - Lists top-rated movies.
   - Navigation to `MovieDetailScreen` is available for detailed views.

3. **MovieDetailScreen**
   - Shows detailed information about a selected movie, including IMDB rating.
   - Accessed from both Home and Top Rated screens.

4. **SearchScreen**
   - Provides search functionality to find movies by name.
   - Displays search results in a list format.

## Error Handling

Handling errors effectively is crucial for a smooth user experience. Here’s how Moviesaya manages errors:

### Common Error Types

1. **Network Errors**
   - Occurs when there is no internet connection or the TMDb API server is unreachable.
   - **Solution**: Display a user-friendly message indicating connectivity issues.

2. **API Errors**
   - Includes invalid API keys, rate limiting, or incorrect endpoint usage.
   - **Solution**: Handle different status codes and show appropriate messages.

3. **Data Errors**
   - Occurs if API responses have unexpected data formats or missing fields.
   - **Solution**: Use default values or error boundaries to prevent app crashes.

### Error Handling Example

Here’s how you can handle errors while fetching movie data:

```javascript
const fetchMovies = async (endpoint) => {
  try {
    const response = await fetch(endpoint);
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    const data = await response.json();
    return data.results;
  } catch (error) {
    console.error('Error fetching movies:', error);
    alert('An error occurred while fetching movie data. Please try again later.');
    return [];
  }
};
```

### Displaying Error Messages

Utilize components or hooks to display errors:

```javascript
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

const ErrorComponent = ({ message }) => (
  <View style={styles.errorContainer}>
    <Text style={styles.errorText}>{message}</Text>
  </View>
);

const styles = StyleSheet.create({
  errorContainer: {
    alignItems: 'center',
    justifyContent: 'center',
    marginTop: 20,
  },
  errorText: {
    color: 'red',
    fontSize: 16,
  },
});

export default ErrorComponent;
```

Use this component within screens to handle and display errors.

## Troubleshooting

### Common Issues and Solutions

1. **App Not Starting**
   - **Issue**: Errors during the app startup.
   - **Solution**: Ensure dependencies are installed with `npm install` or `yarn install`, and check for any syntax errors in the code.

2. **API Key Invalid**
   - **Issue**: Incorrect or expired TMDb API key.
   - **Solution**: Verify the API key in the `.env` file and ensure it is correctly applied within the app.

3. **Blank Screen**
   - **Issue**: UI not rendering due to errors.
   - **Solution**: Check the console for errors and inspect component render logic.

4. **Slow Performance**
   - **Issue**: App running slowly on devices.
   - **Solution**: Optimize images, reduce API calls, and use tools like [React Native Debugger](https://github.com/jhen0409/react-native-debugger) for performance profiling.

### Debugging Tips

- **Console Logs**: Use `console.log` to debug values and application flow.
- **React Native Debugger**: A powerful tool to debug and optimize React Native apps.
- **Emulator Logs**: Check logs from Android Studio or Xcode for native errors.

## Contributing

We welcome contributions from the community! Follow these steps to contribute:

1. Fork the repository on GitHub.
2. Create a new branch for your feature or bugfix.
3. Implement your changes and commit them with descriptive messages.
4. Push your changes to your forked repository.
5. Open a pull request against the main repository.

### Code Style Guidelines

- **JavaScript Standard Style**: Adhere to the standard coding style for JavaScript.
- **Component Reusability**: Design components to be reusable and maintainable.
- **Commenting**: Add comments to explain complex logic or algorithms.

## License

Moviesaya is licensed under the MIT License. You are free to use, modify, and distribute this software following the license terms.

---

## Contact Information

For further assistance or inquiries, please contact me

- **Email**: kymrhys@gmail.com
- **GitHub**: [Moviesaya GitHub Repo](https://github.com/kymrhys2k22/moviesaya)


---
