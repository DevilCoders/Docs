Docker image for Maps Core Mobile Proxy load testing upstream

# Updating dependencies
```bash
svn up (Arcadia Root Dir)/maps/infra/baseimage
```

# Building
```bash
cd (Arcadia Root Dir)/maps/mobile/server/proxy-load-upstream/docker
ya package pkg.json --docker --docker-network=host --docker-save-image
```

# Building and pushing
```bash
cd (Arcadia Root Dir)/maps/mobile/server/proxy-load-upstream/docker
ya package pkg.json --docker --docker-network=host --docker-save-image --docker-push
```
