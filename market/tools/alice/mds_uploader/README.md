# Тулза для заливки данных в mds для Маркета в Алисе

## Как скачать ключи
Для начала работы нужно получить ключи. Это делается командой `mds_upload get_keys -t <токен mds> -e <testing|production> -i 2536 -o <файл куда записать ключи>`. Ссылки на получение токенов есть вот [здесь](https://wiki.yandex-team.ru/mds/s3-api/authorization/#upravlenieaccesskeys). Важно использовать соответсвующий токен с соответствующим окружением (testing-production). Файл с ключами для тетинга и продакшна тоже должны быть разными. Данную команду нужно выполнить только один раз.

## Как выставить интервалы бесплатной доставки (MALISA-356)
Для выставления дат нужно выполнить `mds_upload set_delivery_dates -k <файл, куда записали ключи> -e <testing|production> -f <дата начала> -t <дата конца>`. Дата начала и конца указываются в формате ISO. Например `2018-11-07T11:35:00+03:00`.

Проверить изменения можно просто сходив по следующим урлам курлом или браузером: [тестинг](http://market-in-alice.s3.mdst.yandex.net/free_delivery_interval) и [прод](http://market-in-alice.s3.mds.yandex.net/free_delivery_interval). По этим урлам изменеия должны появляться мгновенно. Басс будет обновлять эту информацию в течении 10 минут.

## Как обновить файлы (стоп-категории, стоп-слова, промо акции)
Сначала нужно скачать текущий файл

`mds_upload load_file -n <stop_categories|stop_words> -e <testing|production> -f <файл вывода>`


Затем стоит изменить содержимое файла и залить новые данные в mds

`mds_upload set_file -n <stop_categories|stop_words> -k <файл, куда записали ключи> -e <testing|production> -f <файл>`


Проверить изменения можно просто сходив по следующим урлам курлом или браузером:

Стоп слова:
[тестинг](http://market-in-alice.s3.mdst.yandex.net/words/content) и [прод](http://market-in-alice.s3.mds.yandex.net/words/content).

Стоп категории:
[тестинг](http://market-in-alice.s3.mdst.yandex.net/categories/content) и [прод](http://market-in-alice.s3.mds.yandex.net/categories/content).

Промо акции:
[тестинг](http://market-in-alice.s3.mdst.yandex.net/promotions) и [прод](http://market-in-alice.s3.mds.yandex.net/promotions).

По этим урлам изменения должны появляться мгновенно. Басс будет обновлять эту информацию в течении 10 минут.

## Добавление фактов от слободы
1) получаем mds ключи (и созраняем в testing.mds-keys)
2) `./mds_uploader load_file -n promotions -e testing -f promos.json` # если файла promos.json не было, он создастся, иначе перезапишется
3) Правим файл
4) `./mds_uploader set_file -n promotions -e testing -k testing.mds-keys -f promos.json`

### Пример файла promos.json
```
{
    "free_delivery_interval": {...}, // оставляем как было
    "free_delivery_by_vendor": {...}, // оставляем как было

    "sloboda": {
        "facts": [
            {
                "key_words": ["молоко", "молочко", "литр молока"], // если добавляется одна из этих строчек в список покупок, значит должны ввывести один из фактов
                "texts": ["молоко оч полезное, вкусное и вообще зашибись", "не советуем питьь прокисшее молоко"]
            },
            {
                "key_words": ["лапша", "лапшичка", "вермишель"],
                "texts": ["факт 1", "факт 2", "факт 3"]
            }
        ]
    }
}
```
