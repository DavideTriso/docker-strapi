# Docker Strapi

Image to run the Strapi CMS in a containerized environment.

## Quick reference

### Build the image:

```
docker build -t davidetriso/strapi:[tagname-dir_name] ./[tagname-dir_name]
```

E.g.:

```
docker build -t davidetriso/strapi:node-18.18 ./node-18.18
```

### Push image to Docker Hub

```
docker push davidetriso/strapi:tagname
```

E.g.:

```
docker push davidetriso/strapi:node-18.18
```

###  Build and push everything

Execute the `./build-and-push.sh` script to build and push all images to Docker Hub at once.

## How to use

Mount your app code in the `/app` dir inside the container using bind mounts; the `node_modules` and `.next` directories can be excluded, because they will be populated by the image in runtime.

For example, in a compose file add:

```yaml
volumes:
    - ./:/app
    # exclude the node_modules and .next directories with 'empty' mounts
    - /app/node_modules
    - /app/.next
```

By default the image will start a production server.
To start the application in dev mode, set the `ENV` var to `dev`.

For example, in a compose file add:

```yaml
environment:
    ENV: dev
```

> NOTE: When the container starts, if there is no package.json file in the /app directory, the entrypoint script will initiate the creation of a new Strapi application with default configurations and install the MySQL package as a project dependency.

## License

Licensed under the terms of the [MIT](LICENSE) license.