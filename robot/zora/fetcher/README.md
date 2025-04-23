# Ручное тестирование
Запуск фетчера из корня Аркадии:
`robot/zora/fetcher/main/fetcher -c robot/zora/conf/static/cloud/test/fetcher.pb.txt --source-config-path robot/zora/conf/dynamic/cloud/test/sources.pb.txt`
Для тестирования нужна утилита grpcurl https://github.com/fullstorydev/grpcurl
Пример запуска:
`grpcurl -vv -d @ -plaintext -proto  robot/zora/fetcher/api/fetcher_service.proto  '[::]:9090' NZora.NFetcher.TFetcherService/Fetch <robot/zora/fetcher/test/request.json`