# vertis/buildbox-buildpkg Dockerfile

## Usage

Supposing cwd is the debian package root.

~~~dockerfile
FROM registry.yandex.net/vertis/buildbox-buildpkg:1.trusty

COPY debian/control /var/lib/buildd/workspace/debian/control
RUN apt-get update \
  && mk-build-deps -i -r -t 'apt-get -y' /var/lib/buildd/workspace/debian/control
COPY . /var/lib/buildd/workspace

CMD ["buildbox-buildpkg", "--debbuildopts", "-b -us -uc", "--buildresult", "buildpkg_artifacts"]
~~~

### Onbuild

~~~dockerfile
FROM registry.yandex.net/vertis/buildbox-buildpkg:1.trusty-onbuild
~~~
