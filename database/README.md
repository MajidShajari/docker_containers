# Database Stack with PostgreSQL, PgAdmin, MongoDB, and Mongo Express
This project deploys a complete database management environment using **Docker Compose**.  
All services are isolated from the outside world and only accessible via **Nginx Proxy Manager** (NPM).

---
## 📦 Services
1. **PostgreSQL** – Relational database
2. **PgAdmin** – Web-based PostgreSQL administration
3. **MongoDB** – NoSQL database
4. **Mongo Express** – Web-based MongoDB administration

---
## 📁 Project Structure

```
.
├── docker-compose.yml
└── .env
```
---
## ⚙️ Environment Variables
Create a `.env` file in the project root with the following content:
```env
# PostgreSQL
POSTGRES_DB=postgres
POSTGRES_USER=admin
POSTGRES_PASSWORD=secretpassword

# PgAdmin
PGADMIN_DEFAULT_EMAIL=admin@example.com
PGADMIN_DEFAULT_PASSWORD=secretpassword

# MongoDB
MONGO_ROOT_USER=root
MONGO_ROOT_PASS=secretpassword
MONGO_DB=mydb

# Mongo Express
ME_BASIC_USER=admin
ME_BASIC_PASS=secretpassword
```
> **Note:** Change all default passwords before deploying.
---
## 🚀 Deployment
1. Make sure **Docker** and **Docker Compose** are installed on your server.
2. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>
   ```
3. Create the `.env` file as shown above.
4. Start the services:
   ```bash
   docker compose up -d
   ```
5. Verify that all containers are running:
   ```bash
   docker ps
   ```
---
## 🌐 Access via Nginx Proxy Manager
All web UIs (**PgAdmin** and **Mongo Express**) are exposed only on the internal `npm_net` network.  
To access them:
1. Open **Nginx Proxy Manager**.
2. Create a **Proxy Host** for each service:
   - **PgAdmin**:  
     - Domain: `pgadmin.example.com`  
     - Forward Hostname/IP: `PgAdmin`  
     - Forward Port: `80`
   - **Mongo Express**:  
     - Domain: `mongo.example.com`  
     - Forward Hostname/IP: `MongoDB-Express`  
     - Forward Port: `8081`
3. Enable SSL (Let's Encrypt) if desired.
---
## 🔒 Security Notes
- Databases are **not** exposed to the internet (`ports` are not published).
- Access to web UIs is secured via **NPM** and **basic authentication**.
- Always use **strong passwords** and **HTTPS**.
---
## 🛑 Stopping the Stack
```bash
docker compose down
```
To remove all data volumes as well:
```bash
docker compose down -v
```
---
## 🧾 License
MIT License
