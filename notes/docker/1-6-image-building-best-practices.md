## Image-building best practices

### Security scanning

> you must be logged in to Docker Hub to scan your images.
> run the command `docker scan --login`, and then scan your image `docker scan <image-name>`

### Image layering

> you can look at what makes up an image
> using `docker image history` command, you can see the command that was used to create each layer within an image.
- each of the lines represents a layer in the image.
- using this, you can quickly see the size of each layer, helping diagnose large images.
- get the full output
  `docker image history --no-trunc getting-started`

### Layer caching

> decrease build times for your container images.

> once a layer changes, all downstream layers have to be recreated as well.

> each command in the Dockerfile becomes a new layer in the image.

> restructure Dockerfile help support the caching of the dependencies.

```Dockerfile
FROM node:12-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```
- we made a change to the image, the yarn dependencies had to be reinstalled.

- fix that, we could first copy `package.json`, install the dependencies, and then copying everything else.

```Dockerfile
FROM node:12-alpine
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install --production
COPY . .
CMD ["node", "src/index.js"]
```

#### .dockerignore
- `.dockerignore` file are an easy way to copy only image relevant files.
- in this case, the `node-modules` should be omitted in the sencon `COPY` step.

- `docker build -t getting-stared .`
