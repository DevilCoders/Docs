# Migration

Try to use [wiki-dump](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/sbin/wiki_dump) to simplify migration from wiki:

    ./wiki-dump -wiki-cluster /runtime-cloud/rtc-support/

It can convert some subset of wiki syntax to markdown and download files from wiki.

# Development

For local dev you can use this recipe:

    npm -g install static-server
    make clean && make web

# Deploy

Simply merge you PR to trunk.

# Links
* [Docs](https://docs.yandex-team.ru/rtc/)
* [Metrika](https://metrika.yandex.ru/dashboard?id=71770390)
* [WikiDump](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/sbin/wiki_dump)
* [YFM](https://github.com/yandex-cloud/yfm-transform/blob/master/DOCS.md)
