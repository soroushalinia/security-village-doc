# Docker

There is an compose file (`docker-compose.yaml`) inside the source code that can be used with docker to deploy the
application with docker easily though you can directly use source code to deploy it without docker.

`.env` file should be ready from the first step in this method. See [Secrets](./secrets.md)

Then you can use docker compose to run all required services:

```shell
docker compose up --build
```