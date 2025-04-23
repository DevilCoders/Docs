# Apt dependency resolution tool
## Requirements

Ubuntu linux (tested on 18.04 and 16.04) with following packages installed:
* python-yaml
* python-apt
* python2.7


    sudo apt-get install python-apt python-yaml python2.7


User running `pkg_tool` must also have passwordless `sudo`.


    usage: pkg_tool.py [-h] -s SELECTIONS -d DUMP -r ROOT [--skip-cleanup]
                       [--distro DISTRO]
    
    optional arguments:
      -h, --help            show this help message and exit
      -s SELECTIONS, --selections SELECTIONS
                            selections yaml
      -d DUMP, --dump DUMP  dump computed selections to file
      -r ROOT, --root ROOT  temporary apt root dir
      --skip-cleanup        Do not remove temporary apt root
      --distro DISTRO       Distro (xenial, focal, etc...)

## Alternative run method: Docker
pkg_tool intended to run in Docker like this:

    docker build -t pkg_tool . && docker run -it --rm -v $(realpath .):/data pkg_tool -s selections.yaml -d computed.yaml

Entrypoint wrapper script prepends all relative paths (not starting with "/" and "-") with /data/
so you can use relative paths from current directory without prepending /data/ on command line.

## Usual workflow
* Update `rtc-xenial|focal-prod-selections.yaml` with desired changes
* Commit `rtc-xenial|focal-prod-selections.yaml` to arcadia (remember revision)
* Run `pkg_tool` to generate full selections


        docker build -t pkg_tool . && docker run -it --rm -v $(realpath .):/data pkg_tool -s rtc-xenial|focal-prod-selections.yaml -d computed-xenial|focal.yaml


* Run hostctl.py to generate upstream-packages unit


        python3 hostctl.py -v '<remembered revision>' -f computed-focal.yaml -x computed-xenial.yaml -o upstream-packages.yaml


* Push upstream-packages unit to cluster


        hmctl push -r core -m '<commit message> -c <cluster> upstream-packages.yaml


