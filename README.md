# Sample RESTful Web Service Project in Go

## Table of Contents
1. [General Info](#general-info)
2. [Project Structure](#project-structure)
3. [Technologies](#technologies)
4. [How to Run](#how-to-run)
5. [API Endpoints](#api-endpoints)
6. [Contribution](#contribution)

## General Info
***
This project is a RESTful web service written in Go that provides CRUD (Create, Read, Update, Delete) operations for users and posts. It uses PostgreSQL as the underlying database and Docker for containerization.

## Project Structure
***
- **`database/`:** Contains the Dockerfile and SQL script for setting up the PostgreSQL database.
    - **Dockerfile:** Defines the Docker image for the PostgreSQL database. It copies the up.sql SQL script to initialize the database schema and starts the PostgreSQL server.
    - **postgres.go:** Defines the PostgreSQL repository that handles the database operations. It includes functions to insert users and posts, retrieve users and posts by ID or email, update posts, delete posts, and list posts with pagination.
    - **up.sql:** Contains the SQL statements to create the `users` and `posts` tables in the database.
- **`handlers/`:** Contains the HTTP request handlers for different API endpoints.
    - **home.go:** Defines the handler for the home *("/home")* endpoint. It returns a JSON response with a welcome message.
    - **post.go:** Defines the handlers for the post-related endpoints *("/posts")*. It includes handlers to create a new post, retrieve a post by ID, update a post, delete a post, and list posts with pagination.
    - **user.go:** Defines the handlers for the user-related endpoints *("/users")*. It includes handlers to register a new user and login.
- **`middleware/`:** Contains the authentication middleware for verifying JWT tokens.
    - **auth.go:** Defines the authentication middleware that checks for valid JWT tokens. It includes a list of endpoints that do not require authentication and a function to validate the token.
- **`models/`:** Contains the data models used in the application.
    - **claims.go:** Defines the custom claims struct for JWT tokens.
    - **post.go:** Defines the model for a post, including its properties.
    - **user.go:** Defines the model for a user, including their email and password.
- **`repository/`:** Contains the repository interface and implementation for database operations.
    - **repository.go:** Defines the repository interface and the implementation of database operations. It includes functions for inserting users and posts, retrieving users and posts by ID or email, updating posts, deleting posts, listing posts with pagination, and closing the connection.
- **`server/`:** Contains the server configuration and setup.
    - **server.go:** Defines the server struct and methods. It includes the server configuration, such as the port, JWT secret, and database URL. It also handles the initialization of the server, binding routes, and starting the HTTP server.
- **`.env`:** Contains the environment variables for the application, such as the port, JWT secret, and database URL.
- **`main.go`:** The entry point of the application. It loads the environment variables, creates a new server instance, and starts the server by binding routes and listening on the specified port.
- **`go.mod`:** The Go module file that specifies the module name and its dependencies.

This structure organizes the project into different packages based on their responsibilities, such as database operations, request handling, middleware, models, and server configuration. It promotes separation of concerns and modularity, making it easier to understand and maintain the codebase.

## Technologies
***
A list of technologies used within the project:

*Make sure to check the links for more information about each technology and library.*
* [Go](): version 1.20
* [JWT](): version 3.2.2+incompatible
* [Gorilla Mux](): version 1.8.0
* [Gorilla WebSocket](): version 1.5.0
* [Godotenv](): version 1.5.1
* [PQ](): version 1.10.9
* [KSUID](): version 1.0.4
* [Go Crypto](): version 0.10.0

These technologies and libraries were instrumental in building the project and implementing essential features such as routing, authentication, database connectivity, and encryption.

## How to Run
***
To run this project, follow these steps:

1. Make sure you have Docker installed on your system.
2. Clone the project repository.
    ```
    $ git clone https://git...
    $ cd ./sample-restful-web-service
    ```
3. Build the Docker image for the database by running the following command:
    ```
    $ docker build -t ***mydatabase*** ./database
    ```
4. Run a container from the created image using the following command:
    ```
    $ docker run –p 54321:5432 ***mydatabase***
    ```
5. Build and run the Go web service by running the following command:
    ```
    $ go run main.go
    ```
6. The API server should now be running at http://localhost:5050 *port defined in the .env file*

## API Endpoints
***
The following API endpoints are available in the project:

- ``GET`` ***/home***: Home endpoint that returns a welcome message.
- ``POST`` ***/users/signup***: Registers a new user by providing the email and password in the request body.
- ``POST`` ***/users/login***: Logs in a user by providing the email and password in the request body. Returns a JWT token.
- ``GET`` ***/me***: Retrieves the authenticated user's details. Requires a valid JWT token in the Authorization header.
- ``POST`` ***/posts***: Creates a new post by providing the post content in the request body. Requires a valid JWT token.
- ``GET`` ***/posts/{id}***: Retrieves a post by its ID.
- ``PUT`` ***/posts/{id}***: Updates a post by its ID. Requires a valid JWT token in the Authorization header.
- ``DELETE`` ***/posts/{id}***: Deletes a post by its ID. Requires JWT token in the header.
- ``GET`` ***/posts***: Lists posts with pagination. Accepts optional page and limit parameters for pagination.

## Contribution
***
Thank you for considering contributing to this project!

Here are some guidelines to help you get involved in the development and contribution of the project:

- If you have any questions or issues related to the project, feel free to open an issue in the repository.
- If you wish to contribute code, we invite you to follow these steps:
    - Fork the repository and clone it to your local machine.
    - Create a new branch from the main branch.
    - Make your modifications and improvements in the new branch.
    - Make sure to write appropriate unit tests for your changes.
    - Run the tests and verify that everything works correctly.
    - Submit a pull request describing your changes and improvements.
- Please make sure to follow the project's code of conduct in all interactions.
- If you have ideas for new features or improvements, you can also share your ideas through issues.

We appreciate all contributions to the project, whether it's through code, issue reports, documentation improvements, or any other form of participation. Thank you again for your interest and contribution!
