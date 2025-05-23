

In this project, we use environment variables in the docker-compose.yaml file to configure the database in a clean, flexible, and secure way:

Purpose of Environment Variables
 - avoid hardcoding sensitive information (like DB usernames and passwords) directly into the docker-compose.yaml file. Instead, values ​​are loaded dynamically from a .env file or during terminal session.

Example of how to use in docker-compose.yaml

services:
  db:
    image: postgres:14
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
	.....

backend:
  environment:
    DB_HOST: db
    DB_USER: ${POSTGRES_USER}
    DB_PASSWORD: ${POSTGRES_PASSWORD}
    DB_NAME: ${POSTGRES_DB}
	.....


This tells Docker to pull the values ​​of POSTGRES_DB, POSTGRES_USER, and POSTGRES_PASSWORD from the environment—usually from a .env file.

Create a .env file in the root folder:

POSTGRES_DB=db-tasks
POSTGRES_USER=user
POSTGRES_PASSWORD=password

Docker Compose automatically loads this file and substitutes the values.

 - backend service (Node.js) also uses similar environment variables to connect to the DB:
 - the same DB credentials are used in both services consistently.
 - enables centralized configuration
 - easy to change credentials
 - more secure (exclude .env from Git using .gitignore)
 - reusable across environments (dev, test, prod)












