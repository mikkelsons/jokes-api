# Joke API

A simple RESTful API built with Node.js and Express to manage and retrieve jokes. The API supports CRUD operations for jokes, filtering by type, and retrieving random jokes. It includes a predefined dataset of 100 jokes categorized by types such as Science, Puns, Wordplay, and more.

### Try the API

**Find the documentation here:**
https://docs.joke-api.smikkelson.dev

## Table of Contents

- [Features](#features)
- [Technologies](#technologies)
- [Installation](#installation)
- [API Endpoints](#api-endpoints)
- [Example Requests](#example-requests)
- [Contributing](#contributing)
- [License](#license)

## Features

- Retrieve a random joke.
- Get a specific joke by ID.
- Filter jokes by type (e.g., Science, Puns).
- Add new jokes.
- Update existing jokes (full or partial updates).
- Delete a specific joke by ID.
- Delete all jokes (requires a master key).
- In-memory joke storage with an initial dataset of 100 jokes.

## Technologies

- **Node.js**: JavaScript runtime for server-side development.
- **Express**: Web framework for building the API.
- **body-parser**: Middleware to parse incoming request bodies.

## Installation

**Clone the repository**:

```bash
git clone https://github.com/your-username/joke-api.git
cd joke-api
```

**Install dependencies**:
Ensure you have Node.js installed, then run:

```bash
npm install express body-parser
```

**Start the server**
Start the server:

```bash
node index.js
```

The server will start on http://localhost:3000.

## API Endpoints

| Method | Endpoint     | Description                            | Parameters/Body                             |
| ------ | ------------ | -------------------------------------- | ------------------------------------------- |
| GET    | `/random`    | Retrieve a random joke                 | None                                        |
| GET    | `/jokes/:id` | Get a joke by ID                       | `id` (path parameter)                       |
| GET    | `/filter`    | Filter jokes by type                   | `type` (query parameter)                    |
| POST   | `/jokes`     | Add a new joke                         | `{ "text": "", "type": "" }`                |
| PUT    | `/jokes/:id` | Replace a joke by ID                   | `id` (path), `{ "text": "", "type": "" }`   |
| PATCH  | `/jokes/:id` | Partially update a joke by ID          | `id` (path), `{ "text"?: "", "type"?: "" }` |
| DELETE | `/jokes/:id` | Delete a joke by ID                    | `id` (path parameter)                       |
| DELETE | `/all`       | Delete all jokes (requires master key) | `key` (query parameter)                     |

### Notes

- The master key for the `/all` DELETE endpoint is `4VGP2DN-6EWM4SJ-N6FGRHV-Z3PR3TT`.
- If a joke ID is not found, the API returns a 404 status with an error message.
- The `/patch` endpoint updates only the provided fields, leaving others unchanged.

## Example Requests

### Get a Random Joke

```bash
curl http://localhost:3000/random
```

**Response**:

```json
{
  "id": 6,
  "jokeText": "How do you organize a space party? You planet!",
  "jokeType": "Science"
}
```

### Get a Joke by ID

```bash
curl http://localhost:3000/jokes/1
```

**Response**:

```json
{
  "id": 1,
  "jokeText": "Why don't scientists trust atoms? Because they make up everything.",
  "jokeType": "Science"
}
```

### Filter Jokes by Type

```bash
curl http://localhost:3000/filter?type=Puns
```

**Response**:

```json
[
  {
    "id": 2,
    "jokeText": "Why did the scarecrow win an award? Because he was outstanding in his field.",
    "jokeType": "Puns"
  },
  ...
]
```

### Add a New Joke

```bash
curl -X POST http://localhost:3000/jokes -d "text=Why did the computer go to art school? Because it wanted to learn to draw a better byte!&type=Tech"
```

**Response**:

```json
{
  "id": 101,
  "jokeText": "Why did the computer go to art school? Because it wanted to learn to draw a better byte!",
  "jokeType": "Tech"
}
```

### Delete All Jokes

```bash
curl -X DELETE "http://localhost:3000/all?key=[MASTER-KEY]"
```

**Response**:

```http
200 OK
```
