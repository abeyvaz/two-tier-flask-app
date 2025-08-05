Here's a beautified and well-formatted version of your **GitHub README** for the Flask app with MySQL Docker setup:

---

# 🚀 Flask App with MySQL – Dockerized Setup

This is a simple **Flask web application** that connects to a **MySQL** database. Users can submit messages, which are stored in the database and displayed on the frontend.

---

## 🧰 Prerequisites

Ensure you have the following installed on your system:

* [Docker](https://www.docker.com/)
* [Git](https://git-scm.com/) *(optional, for cloning the repository)*

---

## 📦 Project Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

---

## 🚀 Usage with Docker Compose

### 1. Start the App

```bash
docker-compose up --build -d
```

### 2. Access the App

* **Frontend**: [http://localhost](http://localhost)
* **Backend (API)**: [http://localhost:5000](http://localhost:5000)

### 3. Create the `messages` Table

You can use any MySQL client or tool (e.g., MySQL CLI, phpMyAdmin) to execute the following SQL:

```sql
CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    message TEXT
);
```

### 4. Interact with the App

* Go to [http://localhost](http://localhost) to view and submit messages.
* Use [http://localhost:5000/insert\_sql](http://localhost:5000/insert_sql) to insert a message directly via backend.

---

## 🧹 Clean Up

To stop and remove all running containers:

```bash
Ctrl + C   # In terminal where docker-compose is running
```

Or run:

```bash
docker-compose down
```

---

## 🐳 Running Without Docker Compose

### 1. Build the Flask App Image

```bash
docker build -t flaskapp .
```

### 2. Create a Docker Volume

```bash
docker volume create two_tier
```

### 3. Create a Docker Network

```bash
docker network create my-net
```

### 4. Start the MySQL Container

```bash
docker run -d \
    --name mysql \
    -v two_tier:/var/lib/mysql \
    --network=my-net \
    -e MYSQL_DATABASE=twotier_db \
    -e MYSQL_ROOT_PASSWORD=root \
    -e MYSQL_PASSWORD=root \
    -p 3306:3306 \
    mysql:5.7

docker run -d --name mysql -v two_tier:/var/lib/mysql --network=my-net -e MYSQL_ROOT_PASSWORD=root -e MYSQL_PASSWORD=root -e MYSQL_DATABASE=twotier_db -p 3306:3306  mysql:5.7
```

### 5. Start the Flask App Container

```bash
docker run -d \
    --name flaskapp \
    --network=my-net \
    -e MYSQL_HOST=mysql \
    -e MYSQL_USER=root \
    -e MYSQL_PASSWORD=root \
    -e MYSQL_DB=twotier_db \
    -p 5000:5000 \
    flaskapp:latest

docker run -d -p 5000:5000 --name flaskapp --network=my-net -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=root -e MYSQL_DB=twotier_db flaskapp:latest
```

---
🐬 Connect to MySQL Container and Check Table
🔹 1. Enter MySQL Container
bash
Copy
Edit
docker exec -it mysql bash

## 📝 Notes

* Ensure the database and table are created before testing the app.
* If you need to reinitialize your database, you can modify or add SQL files in the `docker-entrypoint-initdb.d` directory (if using `docker-compose`).

---

## 📂 Directory Structure

```bash
your-repo-name/
├── app.py
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
└── message.sql   # Optional: Prepopulate schema/table
```

---



