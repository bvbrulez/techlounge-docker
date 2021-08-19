# Folge 4: Images bauen

- [Video der Folge 4: Images bauen](https://www.thenativeweb.io/learning/techlounge-docker)

In der vierten Folge wird das erste eigene Image gebaut.

## Workspace erstellen

Beispiel-Applikation mit Express erstellen.

```shell
$ mkdir hello
$ cd hello
```

## Express-Applikation erstellen

Die Beispiel-Applikation mit `npx` und dem Express-Generator erstellen:

```shell
$ npx express-generator
```

Alternativ mit Docker erstellen:

- Nodejs wird damit nicht auf dem Computer benötigt

```shell
# -v oder --volume mountet ein Host-Verzeichnis im Container
# --name setzt den Namen des Containers
$ docker run -v "$(pwd):/hello" --name name_des_containers node:lts-alpine ls /hello
# -w oder --workdir setzt das aktuelle Verzeichnis im Container (eine Art "ls", damit wird direkt in das Verzeichnis im Container gegangen)
$ docker run -v "$(pwd):/hello" -w /hello node:lts-alpine npx express-generator
```

## Dockerfile

- File erstellen

```shell
$ touch Dockerfile
$ vi Dockerfile
```


```dockerfile
FROM node:lts-alpine
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
EXPOSE 3000
CMD [ "npm", "start" ]
```

## Image bauen

```shell
$ docker build -t hello .
```

## Applikation starten

```shell
$ docker run -d -p 8080:3000 hello
```

Im Browser öffnen: http://localhost:8080

## Eigenes Image auf den Docker Hub

```shell
$ docker login
$ docker tag hello dockerid/hello
$ docker push dockerid/hello
```

## Wichtige Links der Folge

- [Offizielles Node.js-Image](https://hub.docker.com/_/node)
- [Docker](https://docker.com)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Dokumentation zu Docker Desktop](https://docs.docker.com/desktop)
- [Dokumentation der VSCode Docker Extension](https://code.visualstudio.com/docs/containers/overview)
