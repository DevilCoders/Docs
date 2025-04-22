## Обновление переводов

### Для чего это нужно
[Танкер](https://tanker.yandex-team.ru/project/home) - хранилище переводов. Перловая морда обновляет танкерные переводы с каждым релизом.
А обновление танкерных переводов для `morda-go` [пока](https://st.yandex-team.ru/HOME-70334) происходит в ручном режиме.

### Что нужно сделать:
* На виртуальной машине обновить `trunk` любого инстанса перловой морды
* Переименовать файл с переводами:
`
cp auto/Lang_auto.json auto/lang.json
`
* Загрузить файл `lang.json` в Sandbox:
`
  ya upload auto/lang.json --owner HOME --ttl inf -d 'Morda tanker translates DD.MM.YYYY'
`
* Скопировать номер ресурса `resource id` из консоли, например `3345645618`
* Обновить номер ресурса для `morda-go` в файле [portal/avocado/libs/utils/lang/ya.make](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/lang/ya.make?rev=r8872104#L10)
* Закоммитить обновленный `lang/ya.make` в `trunk`
