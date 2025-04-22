### Installing

Put `mana` to `~/bin/mana` and add `~/bin` to your `$PATH` if needed.

### Usage

The script will read the `mana.conf` file and launch every command as well.

Feel free to check out an example file from `manascript/mana.conf`


*To launch an app`:*
```bash
mana launch 
```

*To build without launching`:*
```bash
mana build
```

*To build and launch using `manage.py`:*
```bash
mana manage [params]
# e.g.
mana manage shell
```

*To build and launch using `gunicorn.py`:*
```bash
mana launch [params]
# e.g.
mana launch --config=./etc/gunicorn/config.dev.py
```

*Just launch a previous build with `manage.py`:*
```bash
mana [params]
# e.g.
mana shell
```

*Build binaries:*
```bash
mana build
```

*Build a package:*
```bash
mana package
# or
mana pkg
```

*Build docker:*
```bash
mana docker 
```

*Build and run docker:*
```bash
mana docker run
```

*Build and publish docker to yandex registry:*
```bash
mana docker push

# or if you haven't logged in to yandex registry
mana docker push -l
# or
mana docker login
```
