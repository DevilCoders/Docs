## Preparation

To use this amazing scripts you should make symlink to **.executerrc**, like this:
    $ln -s $(realpath .executerrc) ~/

May be execute function nead to be fixed for linux

## Usage

    $./pre gds
    $./prod gdf

You can use any alias from **.executerrc**. See **.executerrc** for more info about aliases and parameters

## Hints

Usefull aliases

    $./prod gd_status 
It shows last line in log. There can be two possibilities:
    graph-sas-01.taxi.tst.yandex.net: tskv	timestamp=2020-04-10 14:00:01,699	level=DEBUG	text=Finish graph_downloader
    candidates-sas-01.taxi.tst.yandex.net: tskv	timestamp=2020-04-10 12:34:06,454	level=INFO	text=Start download with command "/usr/local/bin/sky get ... -w rbtorrent:9a59008fc62e2afeea372e97109d62c46a6517fc"
First means, that graph_downloader finish all work, and files must be ready
Second means, that files are still downloading

    $./prod check_version 1586390400
    tracks-graph-sas-01.taxi.dev.yandex.net: drwxr-xr-x 2 root root 4096 апр 10 13:52 1586390400

    $./prod progress 9a59008f
    candidates-myt-02.taxi.yandex.net: 2020-04-10 14:01:56.986 [DEBG] [skybone:m                       ]  [514036:186322]  [res:9a59008f]  progress: 85% (89524206270 bytes done from 104899629086 bytes total) [resid:9a59008f | au | dl   61Mbps | ul   33Mbps]

