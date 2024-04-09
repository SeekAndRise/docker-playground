# Example Voting App

A simple distributed application running across multiple Docker containers.

## Getting started

This solution uses Python, Node.js, .NET, with Redis for messaging and Postgres for storage.

1. Clone the Repository:
```bash
git clone https://github.com/SeekAndRise/docker-playground.git
```

2. Navigate to the Project Directory:
```bash
cd docker-playground/example-voting-app
```

### Manually run voting application Containers

1. Run redis container 
```bash
docker run -itd --name=redis redis
```

2. Run postgres container 
```bash
docker run -itd --name=db -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres portgres:9.4
```

3. Run voting-app and expose it on port 5000
```bash
docker run -itd --name=voting-app --link redis:redis -p 5000:80 dockersamples/examplevotingapp_vote
```

4. Run result-app and expose it on port 5001
```bash
docker run -itd --name=result-app --link db:db -p 5001:80 dockersamples/examplevotingapp_result
```

5. Run worker container 
```bash
docker run -itd --name=worker --link db:db --link redis:redis dockersamples/examplevotingapp_worker
```

The `vote` app will be running at [http://localhost:5000](http://localhost:5000), and the `results` will be at [http://localhost:5001](http://localhost:5001).



### Deploying voting application using Docker Compose


Download [Docker Desktop](https://www.docker.com/products/docker-desktop) for Mac or Windows. [Docker Compose](https://docs.docker.com/compose) will be automatically installed. On Linux, make sure you have the latest version of [Compose](https://docs.docker.com/compose/install/).

Run in this directory to build and run the app:

```bash
docker-compose -f docker-compose.build.yml up
```

The `vote` app will be running at [http://localhost:5000](http://localhost:5000), and the `results` will be at [http://localhost:5001](http://localhost:5001).


## Architecture

![Architecture diagram](architecture.excalidraw.png)

* A front-end web app in [Python](/vote) which lets you vote between two options
* A [Redis](https://hub.docker.com/_/redis/) which collects new votes
* A [.NET](/worker/) worker which consumes votes and stores them in…
* A [Postgres](https://hub.docker.com/_/postgres/) database backed by a Docker volume
* A [Node.js](/result) web app which shows the results of the voting in real time

## Notes

The voting application only accepts one vote per client browser. It does not register additional votes if a vote has already been submitted from a client.

This isn't an example of a properly architected perfectly designed distributed app... it's just a simple
example of the various types of pieces and languages you might see (queues, persistent data, etc), and how to
deal with them in Docker at a basic level.
