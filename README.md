# Inkflow_Whiteboard
InkFlow Whiteboard
InkFlow Whiteboard is a real‑time collaborative whiteboard application.
It combines a Spring Boot backend with a React frontend to provide shared drawing, chat, and session management over WebSockets.

Overview
Create and join whiteboard sessions
Draw and collaborate in real time with multiple users
Chat within a session
Recover sessions and uploaded content
Run locally with in‑memory H2 or PostgreSQL
Ready for containerized and cloud deployment (Docker, Kubernetes, AWS, GCP, Railway, etc.)
Tech Stack
Backend: Java, Spring Boot, WebSocket, REST, Spring Data JPA
Frontend: React (Create React App), HTML5 Canvas, WebSockets
Databases:
H2 (in‑memory) for development
PostgreSQL (local Docker or hosted, e.g. Supabase) for realistic and production use
Build/Tools: Maven Wrapper, npm, Docker, docker‑compose, Kubernetes manifests
Project Structure
whiteboard-app/
Spring Boot backend service (REST + WebSocket, persistence, session/channel logic).
whiteboard-frontend/
React SPA for the whiteboard UI, chat, and session management.
deploy-aws-ecs.sh, deploy-gcloud-run.sh, deploy-kubernetes.sh
Helper scripts and manifests for different deployment targets.
docker-compose.yml, docker-compose.db.yml, Dockerfile
Containers for app and local database.
Prerequisites
JDK 17+ (or the version specified in whiteboard-app/pom.xml)
Node.js and npm (recommended: Node 18+)
Git
Docker and Docker Compose (optional but recommended for local PostgreSQL)
Running the Backend (Spring Boot)
Open a terminal in the project root:

Windows:
cd whiteboard-app
mvnw.cmd spring-boot:run

macOS / Linux:
cd whiteboard-app
./mvnw spring-boot:run

By default, the backend runs in the dev profile using an in‑memory H2 database.

Profiles and databases:

dev (default, in‑memory H2):
mvnw.cmd spring-boot:run
or
./mvnw spring-boot:run

localpg (local PostgreSQL):
SPRING_PROFILES_ACTIVE=localpg mvnw.cmd spring-boot:run
or
SPRING_PROFILES_ACTIVE=localpg ./mvnw spring-boot:run

prod (hosted PostgreSQL, e.g. Supabase):
SPRING_PROFILES_ACTIVE=prod mvnw.cmd spring-boot:run
or
SPRING_PROFILES_ACTIVE=prod ./mvnw spring-boot:run

The backend typically listens on http://localhost:8081 (see application properties if you change ports).

Running Local PostgreSQL with Docker (Optional)
From the project root:

docker compose -f docker-compose.db.yml up -d

This starts a PostgreSQL instance (default user, password, and DB name are configured in docker-compose.db.yml and application-localpg.properties).

When finished:

docker compose -f docker-compose.db.yml down

Running the Frontend (React)
Open another terminal in the project root and install dependencies:

cd whiteboard-frontend
npm install

Configure API URLs (optional but recommended):

Create a file named .env inside whiteboard-frontend with:

REACT_APP_API_URL=http://localhost:8081
REACT_APP_WS_URL=http://localhost:8081/ws

Start the development server:

npm start

Open the app at:

http://localhost:3000

The React dev server proxies API/WebSocket calls to the backend (see setupProxy.js if you adjust ports).

Running Tests
Backend tests:

cd whiteboard-app
mvnw.cmd test (Windows)
./mvnw test (macOS / Linux)

Frontend tests:

cd whiteboard-frontend
npm test

Docker and Deployment
Build and run with Docker (single container or docker‑compose) using:
Dockerfile
docker-compose.yml
Kubernetes deployment manifests are provided in:
k8s-deployment.yaml
Additional deployment helpers:
deploy-aws-ecs.sh
deploy-gcloud-run.sh
deploy-kubernetes.sh
Procfile, railway.json
