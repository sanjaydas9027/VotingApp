# Example Voting App

A simple distributed application running across multiple Docker containers.

## Architecture

![Architecture diagram][architecture.excalidraw.png]

* A front-end web app in [Python](/vote) which lets you vote between two options
* A [Redis](https://hub.docker.com/_/redis/) which collects new votes
* A [.NET](/worker/) worker which consumes votes and stores them in…
* A [Postgres](https://hub.docker.com/_/postgres/) database backed by a Docker volume
* A [Node.js](/result) web app which shows the results of the voting in real time



Access
-  `vote` app at [http://localhost:5000](http://localhost:5000)
-  `results` app at [http://localhost:5001](http://localhost:5001)
