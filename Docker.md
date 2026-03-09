🐳 What is Docker?

Docker is a containerization tool that packages your application with everything it needs (JDK, libraries, configs) and runs it the same way everywhere.

👉 “Works on my machine” problem = solved

Simple example

Without Docker:

Java version mismatch

Missing libs

Different OS issues

With Docker:

App + JDK + dependencies = one container

Runs same on dev / QA / prod

⭐ Why Docker is Important?

✅ Consistent environment

✅ Faster deployment

✅ Lightweight (faster than VM)

✅ Perfect for microservices

✅ Cloud & DevOps friendly

👉 Almost every Spring Boot + Microservices project uses Docker.

🧠 Core Docker Concepts (Interview Focus)
1️⃣ Docker Image

Image = Blueprint / Template

Read-only

Built using Dockerfile

Used to create containers

Example:

docker images


🧠 Analogy:

Image is like a class, container is an object

2️⃣ Docker Container

Container = Running instance of image

Lightweight

Isolated

Can start/stop/delete

Example:

docker run dockerapp
docker ps

3️⃣ Dockerfile

Dockerfile = Instructions to build an image

Example:

FROM amazoncorretto:21-alpine
COPY target/app.jar app.jar
ENTRYPOINT ["java","-jar","app.jar"]


🧠 Interview line:

Dockerfile defines how the image is built.

4️⃣ Docker Engine

Docker Engine = Heart of Docker

Runs containers

Builds images

Talks to OS kernel

Command:

docker info

5️⃣ Docker Desktop

UI + Engine for Windows/Mac

Uses WSL2 in Windows

Required for local development

6️⃣ Docker Hub

Docker Hub = Image repository

Like Maven Central for Docker

Stores images

Example:

docker pull mysql
docker pull amazoncorretto:21

7️⃣ Port Mapping

Maps host port to container port.

docker run -p 8080:8080 dockerapp


🧠 Meaning:

host:container

8️⃣ Volumes

Volumes = Persistent storage

Used for DB data.

Example:

docker volume create myvol


Interview line:

Containers are stateless, volumes provide persistence.

9️⃣ Docker Compose

Runs multiple containers together

Used for:

App + DB

App + Kafka + Redis

Example:

services:
  app:
    image: dockerapp
  db:
    image: mysql


Command:

docker-compose up

🔥 Docker vs Virtual Machine (Very Important)
Docker	Virtual Machine
Lightweight	Heavy
Shares OS kernel	Separate OS
Fast startup	Slow
Less memory	High memory
🚀 Spring Boot + Docker (Amazon Corretto 21)
Step-by-Step from ZERO
🟢 STEP 1: Open your project

Go to your Spring Boot project folder
(the folder that contains pom.xml)

Example:

dockerapp
 ├── src
 ├── pom.xml
 └── target

🟢 STEP 2: Build the JAR

Open Command Prompt / Terminal in this folder and run:

mvn clean package


After success, confirm this file exists:

target/dockerapp-0.0.1-SNAPSHOT.jar


👉 If this JAR is not present, STOP and fix Maven first.

🟢 STEP 3: Create Dockerfile

In the same folder as pom.xml:

Right click → New File

Name it exactly:

Dockerfile


⚠️ No extension (.txt ❌)

🟢 STEP 4: Add Dockerfile content

Open Dockerfile and paste this:

FROM amazoncorretto:21-alpine

WORKDIR /app

COPY target/dockerapp-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]

🧠 What each line means (interview important)

FROM → Java 21 base image

WORKDIR → Container working folder

COPY → Copy JAR into container

EXPOSE → Application port

ENTRYPOINT → Start Spring Boot app

🟢 STEP 5: Build Docker Image

Run this from project root:

docker build -t dockerapp .


You should see:

Successfully built <image-id>


Check image:

docker images

🟢 STEP 6: Run Docker Container
docker run -p 8080:8080 dockerapp


🎉 Your Spring Boot app is now running inside Docker.

🟢 STEP 7: Test Application

Open browser:

http://localhost:8080


(or /hello endpoint)

🟢 STEP 8: Run in background (optional)
docker run -d -p 8080:8080 --name dockerapp-container dockerapp


Check:

docker ps


Stop container:

docker stop dockerapp-container

🔴 Common Errors & Fix
❌ Port already in use
docker run -p 9090:8080 dockerapp

❌ JAR not found

Use wildcard:

COPY target/*.jar app.jar

🎯 Interview One-Liners (Remember)

Image = blueprint

Container = running instance

Dockerfile = instructions to create image

-p host:container = port mapping🚀 Spring Boot + Docker (Amazon Corretto 21)
Step-by-Step from ZERO
🟢 STEP 1: Open your project

Go to your Spring Boot project folder
(the folder that contains pom.xml)

Example:

dockerapp
 ├── src
 ├── pom.xml
 └── target

🟢 STEP 2: Build the JAR

Open Command Prompt / Terminal in this folder and run:

mvn clean package


After success, confirm this file exists:

target/dockerapp-0.0.1-SNAPSHOT.jar


👉 If this JAR is not present, STOP and fix Maven first.

🟢 STEP 3: Create Dockerfile

In the same folder as pom.xml:

Right click → New File

Name it exactly:

Dockerfile


⚠️ No extension (.txt ❌)

🟢 STEP 4: Add Dockerfile content

Open Dockerfile and paste this:

FROM amazoncorretto:21-alpine

WORKDIR /app

COPY target/dockerapp-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]

🧠 What each line means (interview important)

FROM → Java 21 base image

WORKDIR → Container working folder

COPY → Copy JAR into container

EXPOSE → Application port

ENTRYPOINT → Start Spring Boot app

🟢 STEP 5: Build Docker Image

Run this from project root:

docker build -t dockerapp .


You should see:

Successfully built <image-id>


Check image:

docker images

🟢 STEP 6: Run Docker Container
docker run -p 8080:8080 dockerapp


🎉 Your Spring Boot app is now running inside Docker.

🟢 STEP 7: Test Application

Open browser:

http://localhost:8080


(or /hello endpoint)

🟢 STEP 8: Run in background (optional)
docker run -d -p 8080:8080 --name dockerapp-container dockerapp


Check:

docker ps


Stop container:

docker stop dockerapp-container

🔴 Common Errors & Fix
❌ Port already in use
docker run -p 9090:8080 dockerapp

❌ JAR not found

Use wildcard:

COPY target/*.jar app.jar

🎯 Interview One-Liners (Remember)

Image = blueprint

Container = running instance

Dockerfile = instructions to create image

-p host:container = port mapping



OpenShift vs Docker vs Kubernetes (Very Common Interview Question)

These three technologies are used together in modern microservices architecture.


---

1. Docker

Definition:
Docker is a containerization platform used to package an application with all its dependencies into a container so it runs the same everywhere.

Example:

You build a Spring Boot application and create a Docker image.

docker build -t user-service .
docker run -p 8080:8080 user-service

Key Point

Creates containers

Solves “works on my machine” problem



---

2. Kubernetes

Definition:
Kubernetes is a container orchestration platform that manages many containers automatically.

It handles:

Load balancing

Auto scaling

Service discovery

Self-healing pods


Example

If you run 10 microservices containers, Kubernetes manages them.

Example command:

kubectl get pods


---

3. Red Hat OpenShift

Definition:
OpenShift is an enterprise platform built on Kubernetes that adds developer tools, security, and CI/CD automation.

It is developed by Red Hat.

It provides:

Web console

Built-in CI/CD

Security policies

Integrated container registry


Command:

oc get pods


---

Simple Architecture

Developer Code (Spring Boot)
        |
        v
Docker -> Create Container
        |
        v
Kubernetes -> Manage Containers
        |
        v
OpenShift -> Enterprise Platform + CI/CD + Security


---

Simple Real Example (Microservices)

Suppose you have:

User Service

Order Service

Payment Service


Step 1

Create Docker images.

user-service-image
order-service-image
payment-service-image

Step 2

Kubernetes runs them as pods.

Pod1 -> User Service
Pod2 -> Order Service
Pod3 -> Payment Service

Step 3

OpenShift provides

Deployment

UI dashboard

CI/CD pipeline

Security



---

Quick Interview Table

Feature	Docker	Kubernetes	OpenShift

Purpose	Container creation	Container management	Enterprise Kubernetes platform
Developed By	Docker Inc	Google	Red Hat
Main Use	Package app	Orchestrate containers	DevOps platform
Command	docker	kubectl	oc



---

One-Line Interview Answer

Docker → Creates containers
Kubernetes → Manages containers
OpenShift → Enterprise Kubernetes platform with CI/CD and security


---

Interview Follow-up Question

Q: How are they used together in a project?

Answer:

1. Developer builds application.


2. Docker creates container image.


3. Kubernetes deploys containers as pods.


4. OpenShift manages CI/CD, security, and scaling.




---

If you want, I can also explain one very important interview topic next:

“How Spring Boot microservices are deployed in OpenShift using CI/CD pipeline (Git → Jenkins → Docker → Kubernetes → OpenShift)”

This question is frequently asked in Mphasis, TCS, Infosys manager rounds.