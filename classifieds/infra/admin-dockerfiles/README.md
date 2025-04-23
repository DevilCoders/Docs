# vertis dockerfile

An opinionated collection of Dockerfiles for common vsfront tasks.

## Library

See `/library` for the list of available images.

Run `./update.sh [--push] <name>` to build and optionaly push an image from the library.

Example:

```
  › ./update.sh --push nodejs
+ sh generate-dockerfile.sh registry.yandex.net/vertis/nodejs 1.trusty-nodejs4.5.0 1.trusty-nodejs4 1.trusty-lts
+ sudo docker build --rm -t registry.yandex.net/vertis/nodejs:1.trusty-nodejs4.5.0 .
...
+ sudo docker push registry.yandex.net/vertis/nodejs:1.trusty-nodejs4.5.0
sudo: unable to resolve host var01e
The push refers to a repository [registry.yandex.net/vertis/nodejs]
2babfb050e84: Pushed
d4478ea80fd5: Layer already exists
1e5659c2a12a: Layer already exists
975cfa6b20e6: Layer already exists
1.trusty-nodejs4.5.0: digest: sha256:4c08010618b8322d2417e0aba76d1f0b1b9852f802b5c4f9b592d3b07d5783c7 size: 1156
+ sudo docker tag registry.yandex.net/vertis/nodejs:1.trusty-nodejs4.5.0 registry.yandex.net/vertis/nodejs:1.trusty-nodejs4
+ sudo docker push registry.yandex.net/vertis/nodejs:1.trusty-nodejs4
The push refers to a repository [registry.yandex.net/vertis/nodejs]
2babfb050e84: Layer already exists
d4478ea80fd5: Layer already exists
1e5659c2a12a: Layer already exists
975cfa6b20e6: Layer already exists
1.trusty-nodejs4: digest: sha256:4c08010618b8322d2417e0aba76d1f0b1b9852f802b5c4f9b592d3b07d5783c7 size: 1156
```

## Naming conventions

Docker images should be named with the following pattern in mind:

~~~
<yandex-internal-registry>/vertis/<image>:<version>
~~~

- `<yandex-internal-registry>` is `registry.yandex.net`. See [Docker distribuiton](https://wiki.yandex-team.ru/Cocaine/docker-registry-distribution/).
- `<image>` is the name of the image that should represent image purpose. For example `base` is a minimal base image,
  that is used as a top most base layer for other images; `buildbox` is an image to build debian packages; etc.
- `<version>` might be anything that has sense for the particular image.

It's a good practice to version base images so they shows as much useful information as needed.

For example, `registry.yandex.net/vertis/nodejs:1.trusty-nodejs4.3.0` is tagged with the pattern `<v>.<os>-nodejs<node-version>`. From the particular tag it'd trivial to associate the image with os version
and Node.js version.
