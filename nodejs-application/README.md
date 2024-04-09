# Sample Nodejs Application using Docker

This guide will walk you through setting up Nodejs Application using Docker containers.

## Prerequisites

- Docker installed on your machine. You can download and install Docker from [here](https://www.docker.com/get-started).

### Run the following Docker command to build and start NodeJS Application

1. Clone the Repository:
```bash
git clone https://github.com/SeekAndRise/docker-playground.git
```

2. Navigate to the Project Directory:
```bash
cd docker-playground/nodejs-application
```

3. Read Application's Dockerfile
```bash
cat Dockerfile
```

4. Build the Docker Image
```bash
docker build -t nodejs-app:latest .
```

5. Run the Docker Container:
```bash
docker container run -p 3000:3000 nodejs-app:latest
```

6. Access Application
Once both containers are running, you can access the application by navigating to http://localhost:3000 in your web browser.


That's it! You've launched NodeJS application
