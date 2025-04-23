# PHP-проекты AUTO.RU

### Сборка в разработческой среде
```sh
git clone --recursive git@github.com:YandexClassifieds/php.git work
cd work/lib5
./composer update
gen_autoru_phpconfig
sudo service nginx restart
sudo service php7.0-fpm restart
```

Для разработки используется тачка qaphp.dev.vertis.yandex.net
Собирает релизы и катит @timondl  
  
Про процесс:
1. Разработчик пишет код в ветке, делает PR
2. Приходит с веткой или несколькими, которые он хочет катнуть в тестинг, к тестированию
3. Тестирование собирает релизную ветку `release_{date}` из всех веток, которые ему принесли
4. Тестирование катит все в тестинг и прод
5. Только после того, как все доедет до прода тестирование же мержит релизную ветку в масте (вместе с ней замержатся и все остальные)
