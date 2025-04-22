Инструменты для аллоцирование YP подов для шардированных сервисов

./yp_alloc --service-id production-music-match-base-man-yp --cluster MAN --shards-count 40 --nanny-token $(cat /home/nglaz/.nanny_token) --config match-base.conf --allocate-pods --label-shards --deploy-endpoint-sets
