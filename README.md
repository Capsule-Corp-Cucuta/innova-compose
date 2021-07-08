# Innova-Docker-Compose

![Imgur Image](https://i.imgur.com/Vlml12n.png)

This project generate the infrastructure of Innova Web App Project in a Docker architecture.

## Prerequisites

- Install [nodejs](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)

- Install [openjdk](https://openjdk.java.net/install/)

- Install [docker](https://docs.docker.com/engine/install/)

## Preparation

Download the follow repositories:

- [Innova-WEB](https://github.com/Capsule-Corp-Cucuta/innova-web)

- [Innova-API](https://github.com/Capsule-Corp-Cucuta/innova-api)

- [Innova-Compose](https://github.com/Capsule-Corp-Cucuta/innova-compose)

Should be like the follow example:

```
.
├── Innova-WEB
│   ├── src/
│   │   └── ...
│   ├── .gitignore
│   ├── Dockerfile
│   ├── LICENSE
│   ├── README.md
│   ├── angular.json
│   └── package.json
├── Innova-API
│   ├── src
│   │   └── ...
│   ├── .gitignore
│   ├── Dockerfile
│   ├── LICENSE
│   ├── README.md
│   ├── build.gradle
│   └── settings.gradle
└── Innova-Compose
	├── docker-compose.yml
	├── init.sql
	├── LICENSE
	└── README.md
```

Configure your email with 2 steps factor and generate an app password for the follow steps. [here a tutorial](https://youtu.be/nazNO3Ra-_8).

![Imgur Image](https://i.imgur.com/tCc5ai8.png)

Now you should configure the `docker-compose.yml` changing the following environment variables that have `changeit` as value:

- MYSQL_ROOT_PASSWORD (it should the same pass to SPRING_DATASOURCE_PASSWORD)

- SPRING_DATASOURCE_PASSWORD (it should the same pass to MYSQL_ROOT_PASSWORD)

- SPRING_MAIL_SENDER_USERNAME (email configured)

- SPRING_MAIL_SENDER_PASSWORD (app password)

## Build

Into Innova-WEB folder run `npm run build` for generate the angular web app dist.

Into Innova-API folder run `./gradlew assemble` for generate the java api.

Into Innova-Compose folder run `docker-compose build` for build the images.

## Start the server

Into Innova-Compose folder run `docker-compose up -d` for start the Innova Web App Project.

## Configure

Run `docker exec -it innova-db mysql -p` for in to the innova-db container.

Type the password you insert into the docker-compose.yml, for default is `changeit`.

Run `USE innova-db;` for use the schema innova-db.

Run `INSERT INTO users (user_type, id, is_active, address, cellphone, email, lastname, name, password) VALUES ('ADMINISTRADOR', '1090000000', b'1', 'Av 1', '3130000000', 'sergioandresrr@ufps.edu.co', 'Rodriguez', 'Sergio', '$2a$10$aaWTEzvZFRCYw9zXRrfIjefHHtTjx9jzLx3bZYD7oBmvEjS7PO4be');` for insert the ADMIN user.

Run `quit` for go out to the innova-db container.

## Use it

If you follow step by step now you can test Innova Web App Project in [localhost](http://localhost:80/).

The default credentials are:

- email: sergioandresrr@ufps.edu.co

- password: HolaMundo

## Notes

You can skip the entire preparation and build steps by removing the `build: ../API` and `build: ../WEB` lines from `docker-compose.yml`, you only should run `docker-compose up -d` from Innova-Compose folder and it download the latest image of the project but do not forget to configure your email and passwords.
