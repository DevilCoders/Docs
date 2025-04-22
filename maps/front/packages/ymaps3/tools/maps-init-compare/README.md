# Notes

1. We use local docker image based on browserless/chrome for fast chrome configurations.
1. Browserless start ws on 3000 port, so we should pass it to Lighthouse.
1. Produciton ymaps3 has referer checks, we start http-server in docker and add special host to browserless.
