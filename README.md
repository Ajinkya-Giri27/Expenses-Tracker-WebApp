# 🧾 Expenses Tracker WebApp (Dockerized Java + MySQL)

This project demonstrates how to containerize a Java-based Expense Tracker web application using **Docker**, **Docker Compose**, and **Multi-stage Docker builds**.

It includes:

- A Java Spring Boot application
- A MySQL database
- Optimized multi-stage Docker builds
- Docker Compose for service orchestration

## 📖 Introduction

This project shows how to optimize Docker workflows using:

- **Multi-stage Docker builds**: Reduces image size and improves security.
- **Docker Compose**: Simplifies multi-container orchestration.

The application consists of a Java backend and a MySQL database.

---

## 🛠️ Key Technologies

- Java 17 (Spring Boot)
- Maven 3.8.3
- MySQL
- Docker
- Docker Compose

---

## 🚀 Setup Instructions

### Prerequisites

Make sure you have:

- AWS Account
- [Docker & Docker-compose installed
- [Git installed

---

### 1. Clone the Repository

```bash
git clone https://github.com/Ajinkya-Giri27/Expenses-Tracker-WebApp.git
cd Expenses-Tracker-WebApp
```

### 2. Run the Application

Use Docker Compose to build and run the containers:

```bash
docker-compose up --build
```

### 3. Verify

Visit the following URL in your browser:

```bash
http://<your-ec2-public-ip>:8080
```
