# Oladipo Risevest App

### Introduction

This is a RESTful API built using Node.js, Express, TypeScript, Redis and PostgreSQL.

</br>

### Setup

Clone the repository to your local machine.

```bash
git clone https://github.com/dipo0x/risevest-oladipo
```

Ensure that you have NodeJS, PostgreSQL and Redis on your machine. You could use their cloud services.
Navigate to the root directory of the project in a terminal.

```bash
cd risevest-oladipo
```

Run the following command to install the necessary dependencies

```bash
npm install
```

Add a .env file following .env.example file example with the values of each variable

```.env
DATABASE_URL
PORT
NODE_ENV
ACCESSTOKENKEY 
REDIS_HOST
ACCESSTOKENEXPIRESIN
SERVER_NAME
REDIS_PORT
REDIS_PASSWORD
```

</br>

Run the following command run tests

```bash
npm run tests
```

### Running Server

#### Locally

Run the following command to start the server:

```bash
    npm run dev
```

The server will run on http://localhost:3000 by default

</br>

## Available Endpoints

Base URL[dev]: http://0.0.0.0:1500/api/v1

```
### Errors

The response for request failures or any other error are rather simple.

```json
{
    "status": 400,
    "success": false,
    "message": "Post with this title already exist"
}
```

</br>

Query Optimization Task:

```
SELECT u.id, u.name, p.title, c.content
FROM (
    SELECT userId, MAX(createdAt) AS maxCreatedAt
    FROM posts
    LEFT JOIN comments ON posts.id = comments.postId
    GROUP BY userId
    ORDER BY COUNT(posts.id) DESC
    LIMIT 3
) AS top_users
JOIN users u ON top_users.userId = u.id
JOIN posts p ON u.id = p.userId
JOIN comments c ON p.id = c.postId AND c.createdAt = top_users.maxCreatedAt

```
### Conclusion

You can find additional documentation for this API, including request and response signatures, by visiting https://cloudy-firefly-771216.postman.co/workspace/Private-test~483e9aa2-2981-4b0d-ad0b-a023b9c5ad17/collection/24812037-6f15c10a-6c9b-485d-b365-19011010adaa?action=share&creator=24812037 in your web browser.
