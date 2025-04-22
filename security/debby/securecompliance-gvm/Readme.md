# THIS PROJECT IS ORIGINATED FROM https://github.com/Secure-Compliance-Solutions-LLC/GVM-Docker

-----

# Bank instructions

### Docker build image example
`docker build --network host -f dockerfiles/Dockerfile.bank -t registry.yandex.net/security/openvas_yandex_bank_6 .`

### Docker run image example with publishing web ui and not default password
`docker run -it --network host --env PASSWORD="uipass" --rm --name c_openvas_yandex_bank_6 registry.yandex.net/security/openvas_yandex_bank_6`

-----

# Docker build
`docker build --network host -f dockerfiles/Dockerfile.main -t registry.yandex.net/security/openvas_yandex_main .`

# Run docker
1. Place ssl cert to `./secrets/cert.pem`.
2. Run container: `docker run -d --rm --network host --env SYNC_ON_START=true --env PASSWORD="uipass" --env HTTPS=true --env USE_PREGENERATED_SSL=true --volume $(pwd)/secrets:/secrets --volume gvm-data:/data --name openvas_yandex_main registry.yandex.net/security/openvas_yandex_main`
3. Check logs: `docker logs -f openvas_yandex_main`

# Transfer image to another host
1. Build the image: `docker build -t registry.yandex.net/security/openvas_yandex_main .`
2. Export image: `docker save -o /tmp/openvas_yandex_main.tar registry.yandex.net/security/openvas_yandex_main`
3. Transfer image: `scp /tmp/openvas_yandex_main.tar $(REMOTE_HOST):/tmp`
4. Load image on the remote host: `docker load -i /tmp/openvas_yandex_main.tar`

-----

# ORIGINAL README.MD:

-----

[![Docker Pulls](https://img.shields.io/docker/pulls/securecompliance/gvm.svg)](https://hub.docker.com/r/securecompliance/gvm/)
[![Docker Stars](https://img.shields.io/docker/stars/securecompliance/gvm.svg)](https://hub.docker.com/r/securecompliance/gvm/)
[![Gitter](https://badges.gitter.im/Secure-Compliance-Solutions-LLC/gvm-docker.svg)](https://gitter.im/Secure-Compliance-Solutions-LLC/gvm-docker)

![Greenbone Vulnerability Management with OpenVAS](https://github.com/SCS-Labs/Images/raw/main/scs-gvm.png)

This setup is based on Greenbone Vulnerability Management and OpenVAS. We have made improvements to help stability and functionality.

You want to send GVM/OpenVAS results to Elasticsearch, try our [GVM Logstash project](https://github.com/Secure-Compliance-Solutions-LLC/gvm-logstash).

## Documentation
* [View our detailed instructions on gitbook](https://securecompliance.gitbook.io/projects/openvas-greenbone-deployment-full-guide)

If you would like something added to the documentation please create a issue [GVM-Docker Gitbook Repo](https://github.com/Secure-Compliance-Solutions-LLC/gitbook/issues)

## Architecture

The key points to take away from the diagram below, is the way our setup establishes connection with the remote sensor, and the available ports on the GMV-Docker container. You can still use any add on tools you've used in the past with OpenVAS on 9390. One of the latest/best upgrades allows you connect directly to postgres using your favorite database tool. 

![GVM Container Architecture](https://securecompliance.co/wp-content/uploads/2020/11/SCS-GVM-Docker.svg)


## About

We will do our best to conduct all development openly by documenting features and requirements, and managing the project using [issues](https://github.com/Secure-Compliance-Solutions-LLC/GVM-Docker/issues), [milestones](https://github.com/Secure-Compliance-Solutions-LLC/GVM-Docker/milestones), and [projects](https://github.com/Secure-Compliance-Solutions-LLC/GVM-Docker/projects).

<!--
## Dashboard - Sneak peak at our upcoming kibana dashboards

Soon we will release instructions on connecting your OpenVAS vulnerability details to elastic to create dashboards that are interactive and actually work. 

Below is a preview of what we're working on.
![Sneak Peak](https://securecompliance.co/wp-content/uploads/2020/11/dashboard.png)
-->
