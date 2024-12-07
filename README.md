 # Flask App with MySQL Docker Setup

This is a simple Flask app that interacts with a MySQL database. The app allows users to submit messages, which are then stored in the database and displayed on the frontend.

## Prerequisites

Before you begin, make sure you have the following installed:

- Docker
- Docker Compose
- Git (optional, for cloning the repository)

## Setup

1. Clone this repository (if you haven't already):

   ```bash
   git clone https://github.com/Bakhtawarkhan90/Adventure.git
   ```

2. Navigate to the project directory:

   ```bash
   cd Adventure
   ```
## Usage

1. Start the containers using Docker Compose:

   ```bash
   docker-compose down
   docker-compose build
   docker-compose up -d

   ```

2. Access the Flask app in your web browser:

   - Backend: http://localhost:5000
   
## To run this two-tier application using  without docker-compose

- First create a docker image from Dockerfile
```bash
docker build . -t  adventure
```

- Now, make sure that you have created a network using following command
```bash
docker network create  Adventure
```

- Attach both the containers in the same network, so that they can communicate with each other

i) MySQL container 
```bash
docker run -d \
    --name database \
    -v mysql-data:/var/lib/mysql \
    --network= Adventure \
    -e MYSQL_DATABASE=shoot \
    -e MYSQL_USER=root \
    -e MYSQL_ROOT_PASSWORD=kali \
    -p 3306:3306 \
    mysql:5.7

```
ii) Backend container
```bash
docker run -d \
    --name flaskapp \
    --network= Adventure \
    -e MYSQL_HOST=database \
    -e MYSQL_USER=root \
    -e MYSQL_PASSWORD=kali \
    -e MYSQL_DB=shoot\
    -p 5000:5000 \
     adventure:latest

```

3. Access the Flask app in your web browser:

   - Backend: http://localhost:5000

4. Command to Create Table in DB
``` bash
   - CREATE TABLE IF NOT EXISTS contact (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    subject VARCHAR(150),
    message TEXT
);
```

## Notes

- Make sure to replace placeholders (e.g., `your_username`, `your_password`, `your_database`) with your actual MySQL configuration.

- This is a basic setup for demonstration purposes. In a production environment, you should follow best practices for security and performance.

- Be cautious when executing SQL queries directly. Validate and sanitize user inputs to prevent vulnerabilities like SQL injection.

- If you encounter issues, check Docker logs and error messages for troubleshooting.


# Welcome to Adventure! 

## Home Page
![Home Page](./Screenshot%202024-12-07%20122559.png)




