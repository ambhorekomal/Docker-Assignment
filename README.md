# Hello World Node.js Docker Assignment

## Overview

This project is a simple **Node.js + Express application** that returns a "Hello World" message.
The application is containerized using **Docker**, and a **CI/CD pipeline using GitHub Actions** automatically builds and pushes the Docker image to **AWS Elastic Container Registry (ECR)**.

---

## Project Architecture

```
Node.js App
     ↓
Dockerfile
     ↓
GitHub Repository
     ↓
GitHub Actions (CI/CD)
     ↓
AWS Elastic Container Registry (ECR)
```

Whenever code is pushed to the **main branch**, the CI/CD pipeline automatically builds a Docker image and pushes it to AWS ECR.

---

## Tech Stack

* Node.js
* Express.js
* Docker
* GitHub Actions
* AWS ECR

---

## Project Structure

```
Docker-Assignment
│
├── index.js
├── package.json
├── package-lock.json
├── Dockerfile
├── .gitignore
│
└── .github
     └── workflows
          └── ecr-publish.yml
```

---

## Application Code

### index.js

```javascript
const express = require("express");

const app = express();

const PORT = process.env.PORT || 3000;

app.get("/", (req, res) => {
    res.send("Hello from Express server!");
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

---

## Running the Application Locally

Install dependencies:

```
npm install
```

Run the server:

```
npm start
```

Open in browser:

```
http://localhost:3000
```

---

## Docker Setup

### Build Docker Image

```
docker build -t hello-world .
```

### Run Docker Container

```
docker run -p 3000:3000 hello-world
```

Access the application at:

```
http://localhost:3000
```

---

## AWS ECR Integration

The Docker image is pushed to AWS ECR.

Example repository URI:

```
603366204775.dkr.ecr.eu-north-1.amazonaws.com/hello-world
```

---

## CI/CD Pipeline

A GitHub Actions workflow is configured in:

```
.github/workflows/ecr-publish.yml
```

The pipeline automatically:

1. Checks out the repository
2. Configures AWS credentials
3. Logs in to Amazon ECR
4. Builds the Docker image
5. Tags the image using the commit SHA
6. Pushes the image to AWS ECR

This workflow runs on every push to the **main branch**.

---

## GitHub Secrets Required

The following secrets must be configured in the repository:

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_REGION
```

---

## Example Image Tag

Images pushed to ECR are tagged using the commit SHA:

```
hello-world:<commit-sha>
```

Example:

```
hello-world:7a4c19b
```

---

## Author

Komal Ambhore
