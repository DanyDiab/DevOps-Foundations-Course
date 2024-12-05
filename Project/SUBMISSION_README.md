## Multi-Container Docker Application with CI/CD: Calculator App Project

#### Complete Project Instructions: [DevOps Foundations Course/Project](https://github.com/shiftkey-labs/DevOps-Foundations-Course/tree/master/Project)

#### Submission by - **<Dany> <Diab>**

---

### Project Overview

- **Brief project description:**  
  The calculator app is a simple multi-container Docker application that provides both a backend API for calculations and a frontend React web interface for users to interact with. The purpose of this project is to learn some DevOps foundations, such as containerization, service orchestration with Docker Compose, and automation using CI/CD pipelines.

- **Which files are you implementing? and why?:**  
  - **Backend Dockerfile:** To containerize the Python API for performing calculations and ensure consistency in the environment.  
  - **Frontend Dockerfile:** To containerize the React app, making it deployable alongside the backend in any environment  
  - **docker-compose.yml:** To manage and run both the backend and frontend services together as a single application  
  - **GitHub Actions Workflow:** To automate the build, test, and deployment process for both services

- _**Any other explanations for personal note-taking:**_  
    Would have liked to put more effort and better understand the concepts, however I am extremely busy with exams currently. I will certainly work on this more after the exam period is done to practice more

---

### Docker Implementation

**Explain your Dockerfiles:**

- **Backend Dockerfile** (Python API):  
  The backend Dockerfile uses the python:3.9-slim image for a Python environment. It sets the working directory to /app, copies the application code, installs flask and flask_cors using pip, and exposes port 5000. When the container runs, it starts the Flask application using app.py.

- **Frontend Dockerfile** (React App):  
  The frontend Dockerfile is based on the node:14-alpine image for a small Node.js environment. It sets the working directory to /app, copies the code, installs dependencies using npm install, builds the React app with npm run build, and exposes port 3000. The app starts with the npm start command.

**Use this section to document your choices and steps for building the Docker images.**  
Both Dockerfiles are designed to create lightweight, efficient images for the frontend and backend.

---

### Docker Compose YAML Configuration

**Break down your `docker-compose.yml` file:**

- **Services:**  
  - **Frontend:** Runs the React app container, exposing port 3000. It connects to the same network as the backend.  
  - **Backend:** Runs the Flask API container, exposing port 5000.  

- **Networking:**  
  Docker Compose automatically creates a bridge network so both services can communicate using their service names

- **Volumes:**  
  I did not use any volume since persistant data is not needed for a calculator

- **Environment Variables:**  
  - `NODE_ENV` is set to `production` in the frontend.  
  - `FLASK_ENV` is set to `development` in the backend for easier debugging.

**Use this section to explain how your services interact and are configured within `docker-compose.yml`.**  
The frontend sends calculation requests to the API. Both services are connected within the same compose file.

---

### CI/CD Pipeline (YAML Configuration)

**Explain your CI/CD pipeline:**

- **What triggers the pipeline:**  
  The pipeline is triggered by a push or pull_request event on the main branch.

- **Stages:**  
  1. **Frontend Build and Test:** Installs Node.js, runs npm install, runs tests, and builds the React app.  
  2. **Backend Build and Test:** Installs Python, installs Flask dependencies, and runs unit tests.  
  3. **Docker Build and Push:** Builds Docker images for both the frontend and backend, then pushes them to Docker Hub.

- **Docker Image Workflow:**  
  Each service’s Docker image is built during the pipeline, and the images are pushed to Docker Hub for deployment.

**Use this section to document your automated build and deployment process.**  
The pipeline ensures code changes are always tested and the Docker images are updated in the registry.

---

### Assumptions

- The backend Flask API needs flask and flask_cors to work  
- No persistent data is needed for the calculator app

---

### Lessons Learned

- **Challenges:**  
  Setting up proper communication between services in Docker Compose was tricky at first. Learning how to define dependencies in CI/CD workflows was another challenge. After some time I was able to figure out how to proprly set up the workflows.

- **Learnings:**  
  - Learned how to containerize services effectively.  
  - Understood the importance of automation in CI/CD pipelines for reducing manual deployment steps.

**Use this section to reflect on your experience and learnings when implementing this project.**  
 I learned alot about how DevOps is useful to implement better code faster and more effectivly. It was also very interesting and useful to see all of the concepts that I had been learning about over the last 4 weeks coming together to implement a proper CI/CD pipeline.

---

**Use this section to brainstorm ways to enhance your project.**  
I want to implement the error checking and todo lists in the app.js file. The app does not work currently when run in a local port. 

---

**BEST OF LUCK!**
