<i>If you see any unactual information here, please fix it by yourself or with help of your chief/mentor.</i>

Chat: taxi-automatization-support

# Running taxi via Docker

If you're using OS X you can use the [guide](#how-to-install-docker-on-os-x) to install Docker.

## Install docker Ubuntu 16.04+

    sudo apt-get update
    # Installing docker
    sudo apt-get install docker-ce=17.09.0~ce-0~ubuntu
    # Add yourself to docker group
    # but use it only for user desktop workstations!
    # Be careful it could dangerous for clouds
    sudo usermod -aG docker $(whoami)
    # Relogin in system


## Login to docker distribution service
For this you need to get any OAuth token issued in Yandex.
You can get token by following the link:
https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1

After that you must run the following command for docker:

    docker login -u <login> -p <token_body> registry.yandex.net

Or you can run other command:

    docker login -u <login> registry.yandex.net
Paste OAuth token to stdin.

Where token_body is OAuth token.

[If you are unable to login due to permission denied](#solve-docker-login-error)

For more information about this, see the wiki:
https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/#avtorizacija

## Install last version of Docker compose

Install deps-py3

    sudo apt-get update
    sudo apt-get install taxi-deps-py3-2

For MacOS:

    brew install docker docker-compose


Test docker-compose
    
    docker-compose --version

## IPv6 support for docker

It is not necessary to use IPv6 for services in taxi.

But if you need IPv6 support for docker please read the following articles:
https://wiki.yandex-team.ru/taxi/backend/docker-integration-tests/#nastrojjkaipv6vubuntu

## Building images

Reqs:

  * access to dist.yandex.ru:80
  * [ssh agent forwarding](https://wiki.yandex-team.ru/diy/linux/ssh/#generacijaparykljuchejj) if you are working through ssh

Building:

Clone repository to the same directory where your `backend` repository is:

    git clone git@github.yandex-team.ru:taxi/docker-backend.git

And run `make` to build docker images (old stable way)

    make

It will download latest taxi-integration-xenial-base and build base-xenial-image on top of it.

Than you can start containers with run script:

py2:

    ../docker-backend/run taxi-xenial-tests taxi-pytest2 tests-pytest/test_*.py
py3:

    ../docker-backend/run taxi-xenial-tests py.test -vv --ignore tools/

../docker-backend/run by default starts docker-compose with --rm and --service-ports arguments.
You can change it by setting OPTS env variable (default args will be removed completely).

If you want to remove old containers and base images:

    make clean-containers
    make clean-images
    make clean-integration-tests-images

To update taxi-integration-xenial-base and rebuild test images just run make again.

## Run container for tests and run tests using docker-compose

First of all you should install [Docker Compose](#install-last-version-of-docker-compose).

Then, assuming that `backend` and `docker-backend` are in same parent folder:

    username@backend $ ../docker-compose/run taxi-xenial-tests

## Run tests
py2:

    ../docker-backend/run taxi-xenial-tests taxi-pytest2 tests-pytest/test_*.py

Or you can run tests manually from container

> All commands bellow are executed inside the `taxi-xenial-tests` container.

    taxi-pytest2 tests-pytest/test_*.py

## Connecting to MongoDB

If you're using docker-compose to run containers, then 27017 port is exposed to host system, and you can connect to dockerized MongoDB instance from your host system:

    mongo

## How to install Docker on OS X

Nov 2021: You can install Docker Desktop on Mac manually or through Yandex "Self Service" app. 

https://www.unixtutorial.org/docker-desktop-vs-docker-machine/

If something doesn't work, please contact @iv-ivan and use the instructions below.

### Manual install
Before we start you need to install [Homebrew](http://brew.sh/)

Docker daemon can be run only on top of linux distro with cgroups support (OS X is not one of them). To run any suitable distro you need to install VirtualBox (it's easy with Homebrew Cask):

    brew install --cask virtualbox

Then install Docker client:

    brew install docker

And [Docker Machine](https://docs.docker.com/machine/):

    brew install docker-machine

Using Docker Machine we can create new VirtualBox VM with tiny linux distro and Docker daemon on it. And all this things in single command:

    docker-machine create dev --driver virtualbox `# dev is your new Docker Machine name` \
      --virtualbox-cpu-count 2 \
      --virtualbox-host-dns-resolver \
      --virtualbox-disk-size 100000 `# max disk size cause base images are huge` \
      --virtualbox-memory 2048


You may get an error like one below
```bash
This is a known VirtualBox bug. Let's try to recover anyway...
Error creating machine: Error in driver during machine creation: Error setting up host only network on machine start: 
The host-only adapter we just created is not visible. This is a well known VirtualBox bug. 
You might want to uninstall it and reinstall at least version 5.0.12 that is is supposed to fix this issue
```
To fix it you have to go to System Preference -> Security & Privacy -> General and allow installing from Oracle than reboot

Also you may get an error like
```
Error setting up host only network on machine start: /usr/local/bin/VBoxManage hostonlyif ipconfig vboxnet5 --ip 192.168.99.1 --netmask 255.255.255.0 failed:
VBoxManage: error: Code E_ACCESSDENIED (0x80070005) - Access denied (extended info not available)
VBoxManage: error: Context: "EnableStaticIPConfig(Bstr(pszIp).raw(), Bstr(pszNetmask).raw())" at line 242 of file VBoxManageHostonly.cpp
```
To fix it you need to downgrade virtualbox to 6.1.26  <br />
You can download it from https://www.virtualbox.org/wiki/Download_Old_Builds_6_1 

Now you need to configure your local Docker client to work with Docker daemon inside VM. Docker Machine again helps you:

    eval "$(docker-machine env dev)"

This command sets a bunch of environment variables (to see all of them just run: `docker-machine env dev`). Most likely you will want to add this command to your `.bashrc` (`.zshrc`, etc.):

    echo 'eval "$(docker-machine env dev)"' >> ~/.bashrc

To make sure that everything is configured correctly, let's run Hello World :)

    docker run busybox echo 'hello world'

If you see something like this

    ❯ docker run busybox echo 'hello world'
    Unable to find image 'busybox:latest' locally
    latest: Pulling from library/busybox
    cf2616975b4a: Pull complete
    6ce2e90b0bc7: Pull complete
    8c2e06607696: Already exists
    library/busybox:latest: The image you are pulling has been verified. Important: image verification is a tech preview feature and should not be relied on to provide security.
    Digest: sha256:38a203e1986cf79639cfb9b2e1d6e773de84002feea2d4eb006b52004ee8502d
    Status: Downloaded newer image for busybox:latest
    hello world

everything is ok and you can start build [Taxi image](#building-images).

Otherwise you should RTFM or ping [@shmatov](https://staff.yandex-team.ru/shmatov).

### If you have some permissions issues while running tests

Try this:
```
   docker-machine ssh dev \
   "sudo mount -t vboxsf -o uid=$UID Users /Users && \
    echo 'sudo mount -t vboxsf -o uid=$UID Users /Users'  >> /var/lib/boot2docker/bootsync.sh"
```

# backend-cpp
First of all create an image:

    docker-backend $ make build-xenial-image

Again, you need to install [Docker Compose](#install-last-version-of-docker-compose).
Then, assuming that `backend-cpp` and `docker-backend` are in same parent folder:

    backend-cpp $ ../docker-backend/run taxi-xenial-tests

## Building
After cloning `backend-cpp` repository you need to initialize submodules:

    backend-cpp $ git submodule update --init --recursive

To build `backend-cpp` you need to run make:

    backend-cpp $ ../docker-backend/run taxi-xenial-tests make

## Multiprocessor distributed building
Distributed build is disabled by default. To enable distributed build via
[distcc](https://wiki.gentoo.org/wiki/Distcc)
set <b>NPROCS</b> environmental variable equals desired number of jobs.
It's recommended to set it equals doubled number of cores
of your CPU (including Hyperthreading), but you can increase this number
if your system's performance allows.

    backend-cpp $ export NPROCS=8

Run build as usual, but within this terminal session.
## Running tests
To run tests:

    backend-cpp $ ../docker-backend/run taxi-xenial-tests make test

### Solve docker login error

If you are unable to login due to permission denied:

    sudo groupadd docker
    sudo gpasswd -a ${USER} docker
    sudo service docker restart

 more [here](https://www.santoshsrinivas.com/docker-on-ubuntu-16-04/) or
 [docker doc](https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user)

# backend-py3
After cloning `backend-py3` repository you need to initialize submodules:

    git submodule update --init --recursive

Then you can start tests service:

    ../docker-backend/run taxi-xenial-tests ./runtests -vv -x services/{service-name}

or you can use the following command:

    ../docker-backend/run taxi-xenial-tests make test-{service-name}

Example:

    ../docker-backend/run taxi-xenial-tests ./runtests -vv -x services/chatterbox

or:

    ../docker-backend/run taxi-xenial-tests make test-chatterbox

Don't populate databases with fixtures if your application does not require
them:

    ../docker-backend/run taxi-xenial-tests pytest -vv \
        --no-postgresql --no-redis services/taxi-corp/test_taxi_corp/

Check test coverage:

    ../docker-backend/run taxi-xenial-tests pytest -vv \
        --cov=tariffs/tariffs/ --cov-report=html services/tariffs/test_tariffs/

Also you can run all commands within bionic image.

Example:

    ../docker-backend/run taxi-bionic-tests make test-chatterbox

# uservices
First of all create an image.

Create xenial image if your service is in xenial

    docker-backend $ make build-xenial-image

Or create bionic image for bionic services

    docker-backend $ make build-bionic-image

Update submodules:

    uservices $ git submodule update --init --recursive

To run build in xenial image:

    uservices $ ../docker-backend/run taxi-xenial-tests make build-userver-sample

To run tests in xenial image:

    uservices $ ../docker-backend/run taxi-xenial-tests make test-userver-sample

To run build in bionic image:

    uservices $ ../docker-backend/run taxi-bionic-tests make-userver-sample

To run tests in bionic image:

    uservices $ ../docker-backend/run taxi-bionic-tests make test-userver-sample

# Known issues

## backend-py3
`taxi-exp` tests is broken because one of the tests have wrong PostgreSQL path.
