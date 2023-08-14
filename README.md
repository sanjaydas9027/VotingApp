# Example Voting App

A simple distributed application running across multiple Docker containers.

## Architecture

![Architecture diagram](architecture.png)

The application consists of the following components:

- A front-end web app in [Python](/vote) that allows users to vote between two options.
- A [Redis](https://hub.docker.com/_/redis/) container that collects new votes.
- A [.NET](/worker/) worker application that consumes votes and stores them.
- A [Postgres](https://hub.docker.com/_/postgres/) database backed by a Docker volume.
- A [Node.js](/result) web app that displays real-time voting results.

## Access

You can access the app using the following URLs:

- `vote` app: [http://localhost:5000](http://localhost:5000)
- `results` app: [http://localhost:5001](http://localhost:5001)
