# 🚀 Docker Compose Setup: Node.js App + MongoDB  
### (Steps + Commands Only)

---

## ✅ Step 1: Create project folder

```bash
mkdir node-mongo-app
cd node-mongo-app

✅ Step 2: Create Node.js app
mkdir app
cd app

Create server.js
const express = require('express');
const mongoose = require('mongoose');
const app = express();

mongoose.connect('mongodb://mongo:27017/mydb')
    .then(() => console.log("MongoDB Connected"))
    .catch(err => console.log(err));

app.get('/', (req, res) => {
    res.send("Node.js + MongoDB using Docker Compose");
});

app.listen(3000, () => console.log("Server running on port 3000"));

Create package.json
{
  "name": "node-mongo-app",
  "version": "1.0.0",
  "main": "server.js",
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^8.0.0"
  }
}


Go back:

cd ..

✅ Step 3: Create Dockerfile for Node.js

Create file:

app/Dockerfile


Paste:

FROM node:18
WORKDIR /usr/src/app
COPY package.json .
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]

✅ Step 4: Create docker-compose.yml

Create file:

docker-compose.yml


Paste:

version: '3'
services:

  mongo:
    image: mongo
    container_name: mongodb
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db

  app:
    build: ./app
    container_name: node-app
    ports:
      - "3000:3000"
    depends_on:
      - mongo

volumes:
  mongo_data:

✅ Step 5: Start containers
docker compose up -d

✅ Step 6: Check running containers
docker ps

✅ Step 7: Test Node.js app

Open browser:

http://localhost:3000


Expected output:

Node.js + MongoDB using Docker Compose

✅ Step 8: Stop containers
docker compose down

✅ Step 9: Stop + delete MongoDB data
docker compose down -v