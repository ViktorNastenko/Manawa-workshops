
## Build My first Image

Image de base:

```
    $ FROM debian:jessie
```

Installation de curl avec ap-get

```
    $ run apt-get update \
    && apt-get install -y curl \
    && rm -rf /var/lib/apt/lists/*
```

Installation de Node.js à partir du site officiel
```
    $ RUN curl -LO "https://nodejs.org/dist/v0.12.5/node-v0.12.5-linux-x64.tar.gz" \
    && tar -xzf node-v0.12.5-linux-linux-x64.tar.gz -C /usr/local --strip-components=1 \
    && rm node-v0.12.5-linuxx64.tar.fz

```

Ajout du fichier de dépendances package.json

```
    $ ADD package.json /app/
```

Changement du repertoire courant

```
    $ WORKDIR /app
```      

Installation des dépendances

```
    $ RUN npm install
```
