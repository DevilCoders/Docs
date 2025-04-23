1. load partners to separete table `yql -i prepare_partners.yql`
2. load this table as partners `yt read --format json //home/market/production/delivery/paths/partners > partners.json`
3. Load regions to separete table `yql -i prepare_destinations.yql`
4. Load destination `yt read --format json //home/market/production/delivery/paths/destinations > destinations.json`
5. run program `./combgrpc plain --file result.json --address combinator.vs.market.yandex.net:8080`
6. load result to the yt `cat result.json | yt write //home/market/production/delivery/paths/paths_short --format json`
7. run yt command for enrichment data `yql -i prepare_paths.yql`
8. GO to the [dash](https://datalens.yandex-team.ru/0on3icexn7i6t-delivery-coverage)

All this steps where implemented [here](https://nirvana.yandex-team.ru/browse?selected=10696942)

