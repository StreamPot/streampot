# Installation

StreamPot consist of two parts:

-   `@streampot/client` is a JavaScript library that you can use to interact with the server.
-   `@streampot/server` is a CLI tool that you can use to launch the server.

## Setting up the client

::: code-group

```sh [npm]
$ npm add -D @streampot/client
```

```sh [pnpm]
$ pnpm add -D @streampot/client
```

```sh [yarn]
$ yarn add -D @streampot/client
```

:::

```js
import StreamPot from '@streampot/client';

const client = new StreamPot({
    secret: 'your-api-key',
    baseUrl: 'http://localhost:3000',
});
```

For examples on how to use the client, visit the [examples page](/examples).

## Setting up the server (without Docker)

> [!TIP]
> Instead, you might want to use our [Docker Compose](/docker-compose) template to get started in no time.

### Prerequisites

-   Node.js version 20 or higher.
-   PostgreSQL
-   Redis
-   FFmpeg

### Installation

::: code-group

```sh [npm]
$ npm add -g @streampot/server
```

```sh [pnpm]
$ pnpm add -g @streampot/server
```

```sh [yarn]
$ yarn global add @streampot/server
```

:::

### Starting the server

Create a new `.env` file:

```shell
DATABASE_URL=postgres://postgres:example@db:5432/example
REDIS_URL=redis://redis:6379
S3_ACCESS_KEY=
S3_SECRET_KEY=
S3_REGION=
S3_BUCKET_NAME=
S3_ENDPOINT=
S3_PUBLIC_DOMAIN=
```

> [!WARNING]
> Due to the risks involved in processing user-provided content with ffmpeg encoders, it is recommended that `ffmpeg` is run by spinning up on-demand Docker containers.
>
> To enable this, add the following to your `.env` file:
>
> ```shell
> FFMPEG_STRATEGY=docker
> ```
>
> And pull the ffmpeg image on the system:
>
> ```shell
> docker pull linuxserver/ffmpeg
> ```

Before starting the server, run this command to set-up the database tables:

```sh
$ streampot migrate
```

Now you can start the server:

```sh
$ streampot serve --port=3000
```
