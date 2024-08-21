# Application Deployment

The application, in it's current form, can be deployed to a server using Docker. Both the client and server components come with a Dockerfile that will build these components into Docker images that can be deployed into containers.

## Server Dockerfile

The server Dockerfile generates a Javascript build of the server application that it then hosts. The client Dockerfile is set up with a reverse proxy that will forward requests at a set path to the WebSocket server port (defaults to 8080).

### Environment Variables

Three environment variables can be passed to the server to set the address for the MongoDB server and for what ports the Express and WebSockets server should be made available to.

| Env Variable | Required | Description |
|--------------|----------|-------------|
| `MONGODB_URL` | Yes     | The address to the database. |
| `WSS_PORT`   | No - defaults to 8080 | The port for the WS Server |
| `EXPRESS_PORT` | No - defaults to 3000 | The port for the Express server |

It should be noted that if the WebSocket Server and Express ports are adjusted, these will need to also be adjusted in the Dockerfile and the `compose.yaml` file. Best practice in deployment is to leave the ports as is (and not worry about setting them in the `.env` file), and then change which port is bound to the above ports in the `compose.yaml` file.

## Client Dockerfile

The client Dockerfile has two aims - 1) create a static build of the React (Vite) application, and 2) host the static files using Caddy.

Vite provides a build function that takes the code in its Typescript form and generates static files that can be hosted without need for a responsive server.

### Caddy

Caddy provides that hosting capability, and also provides a reverse proxy for the WebSocket server.

It should be noted that Caddy relies on a Caddyfile being present in the same directory as the Dockerfile. The Caddyfile sets out the domain and/or port that the responses are going to in the first line, and this can be adjusted once a domain is arranged.

Caddy also provides automatic HTTPS. Once a domain has been set up and is accessible, Caddy will automatically generate the HTTPS certificate using Let's Encrypt.

### Enviroment Variables

The client application does not currently rely on any environment variables. However, it should be noted that the path to the WebSocket server is set in the `src/App.tsx` file and has been set up to vary depending on whether the application is running in development or production.

## Docker Compose

A Docker Compose file (`compose.yaml`) is included in the root directory of the project to automatically build and spin up containers for both the server and the client, as well as for MongoDB and Mongo Express (which is basically a GUI for MongoDB).

The whole application can be started up by simply running `docker compose up`. This will automatically build the server and client images (if they haven't been already) and provides a working server.

As the Docker Compose file is currently set up, the different components of the application are accessible on the following ports:

| Component | Port |
|-----------|------|
| Client    | 80   |
| Server    | 3000 (Express), 8080 (WS) |
| MongoDB   | 27018 |
| Mongo Express (ME) | 8081 |

It should be noted each of these ports can be adjusted as desired in the `compose.yaml` file.

### Mongo Express

The Docker Compose file includes a Mongo Express front-end to facilitate access to the database. This component can be safely removed from the file if it is unnecessary once the application is deployed. It is more so included for testing purposes during development.
