🚀 Flask App with MySQL – Dockerized Setup
A simple Flask web application that connects to a MySQL database. Users can submit messages that are stored and displayed dynamically.

🧰 Prerequisites
Make sure the following tools are installed:

Docker

Git (optional, for cloning)

📦 Project Setup
🔹 Clone the Repository
bash
Copy
Edit
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
🚀 Running with Docker Compose
🔹 Start the App
bash
Copy
Edit
docker-compose up --build -d
🔹 Access the App
Frontend: http://localhost

Backend API: http://localhost:5000

🛠️ Creating the messages Table (if not using SQL init file)
Run the following SQL manually to create the table:

sql
Copy
Edit
CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    message TEXT
);
💬 Interact with the App
Visit http://localhost to view and submit messages.

Backend endpoint: POST /submit for inserting messages via API.

🧹 Clean Up
To stop and remove containers:

bash
Copy
Edit
docker-compose down
Or stop manually:

bash
Copy
Edit
docker stop flaskapp mysql
docker rm flaskapp mysql
🐳 Run Without Docker Compose
🔹 Build Flask App Image
bash
Copy
Edit
docker build -t flaskapp .
🔹 Create Docker Volume
bash
Copy
Edit
docker volume create two_tier
🔹 Create Docker Network
bash
Copy
Edit
docker network create my-net
🔹 Start MySQL Container
bash
Copy
Edit
docker run -d \
  --name mysql \
  -v two_tier:/var/lib/mysql \
  --network=my-net \
  -e MYSQL_DATABASE=twotier_db \
  -e MYSQL_ROOT_PASSWORD=root \
  -e MYSQL_PASSWORD=root \
  -p 3306:3306 \
  mysql:5.7
🔹 Start Flask App Container
bash
Copy
Edit
docker run -d \
  --name flaskapp \
  --network=my-net \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=root \
  -e MYSQL_DB=twotier_db \
  -p 5000:5000 \
  flaskapp:latest
🐬 Verify MySQL and Tables
🔹 1. Enter MySQL Container
bash
Copy
Edit
docker exec -it mysql bash
🔹 2. Log into MySQL Shell
bash
Copy
Edit
mysql -u root -p
# Enter password: root
🔹 3. Use the Database
sql
Copy
Edit
USE twotier_db;
🔹 4. Show Tables
sql
Copy
Edit
SHOW TABLES;
🔹 5. Check Table Structure
sql
Copy
Edit
DESCRIBE messages;
🔹 6. View Table Data
sql
Copy
Edit
SELECT * FROM messages;
🔹 7. Exit
sql
Copy
Edit
exit;   -- Exit MySQL shell
exit    -- Exit container shell
📝 Notes
Make sure your table is created before using the app.

You can initialize the DB automatically using message.sql placed in the docker-entrypoint-initdb.d directory (already mapped in docker-compose.yml).

📁 Project Structure
bash
Copy
Edit
your-repo-name/
├── app.py                     # Flask application
├── Dockerfile                 # Dockerfile for Flask app
├── docker-compose.yml         # Docker Compose file
├── requirements.txt           # Python dependencies
└── message.sql                # SQL init script (optional)


