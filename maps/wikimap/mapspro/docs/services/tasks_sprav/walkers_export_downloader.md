# wiki-walkers-export-downloader
Процесс заливки фотографий, сделанных пешеходами для Яндекс.Бизнеса, в подложку НК, и генерации гипотез по ним.

# Исходные данные
Исходные данные - таблицы на YT:

* Экспорт фоток для POI ```//home/sprav/assay/tasker/walkers/export```
* Данные по фотографиям, загруженным с мобильных устройств ```//home/sprav/assay/tasker/walkers/v3/yang_mobile_photos```
* Данные по фотографиям, загруженным с ПК ```//home/sprav/assay/tasker/walkers/v3/yang_desktop_photos```
* Данные по фотографиям в Raw-формате, загруженным с ПК ```//home/sprav/assay/tasker/walkers/v3/yang_raw_desktop```
* Экспорт всех публикуемых компаний из Яндекс.Бизнеса ```//home/altay/db/export/current-state/exported/company```

# Хранение результата
Данные хранятся в таблицах схемы sprav кластера mapspro_social:

  * ```photo_ids``` url и ID фотографии после загрузки в mrc
  * ```permalink_photo``` ассоциация фотографии и POI
  * ```photo_data``` данные о геопривязке фотографии
  * ```company_bundle``` пакеты данных о компании полученные при очередной загрузке
  * ```company_bundle_photo``` состав фотографий пакета.

# Процесс заливки
Уникальным идентификатором для фотографии считается её URL в хранилище.

Таблицы XXX_photos на YT содержат url, дату и координату съёмки.

Таблица raw_desktop содержит url, дату съёмки, набор фотографий (url+тег) и набор координат (тег+координаты). Присутствуют как координаты съёмки, так и объекта.

Таблица export на YT содержит пермалинки и координаты входов в POI.

Данные для фотографий получаются JOIN'ом таблиц по URL.

Фотографии, сделанные больше года назад, игнорируются.

Для каждой фотографии из таблиц XXX_photos определяется координата съёмки как координата входа, если таковая есть, иначе как координата POI.

Для каждой фотографии из таблицы raw_desktop берётся координата съёмки, соответствующая ей по тегу - при условии, что в данных для этой фотографии присутствуют обе координаты (съёмки и объекта).

Если координата не найдена, фотография игнорируется.

Для каждой фотографии с координатой:
1. Происходит заливка в сервис MRC и получение ```photo_id```.
2. Создаётся запись в таблице:
   ```sprav.photo_ids```
    - ```photo_key``` = URL фотографии в хранилище
    - ```photo_id``` = ID фотографии в сервисе MRC
3. На следующем этапе для всех POI происходит поиск и связывание фотографий по URL.
4. Создаётся запись в таблице:
   ```sprav.permalink_photo```
    - ```permalink_id``` = ID POI в Яндекс.Бизнесе
    - ```photo_id``` = ID фотографии в сервисе MRC
    - ```version_id``` = инкрементируемый номер итерации работы процесса для плавного переключения данных для потребителя

Процесс запускается каждые сутки по cron в 7:00.

# Процесс формирования очереди для создания гипотез
Во время каждого запуска загрузки, вновь полученные фотографии для организации складываются в пакет.

Пакет содержит информацию о дате формирования и статус.

Новый пакет создаётся в статусе ```draft``` и переводится в состояние ```waiting``` по завершении формирования.

Если в очереди уже есть пакет в статусе ```waiting``` он дополняется новыми фото.

# Процесс обработки очереди и формирования гипотез
После обновления очереди начинается её обработка

Загружаются самые старые необработанные пакеты

Проверяется статус обработки фотографий

Если не все фотографии обработаны пакет остаётся в очереди

Если все фотографии обработаны и нет годных для публикации, то пакет отменяется

Иначе, создаётся гипотеза с перечислением хороших фотографий.

Источник определяется так:

**experiment-walkers-poi-photo-create** - для гипотез на создание POI, содержит ссылку на **altay**

**experiment-walkers-poi-photo-multi** - если осталась только одна фотография и организация уже есть в НК

**experiment-walkers-poi-photo-single** - если осталась больше одной фотографии и организация уже есть в НК

Видимость гипотез зависит от видимости фотографий

В доработке
Основные пункты
  * Мониторится длинна очереди и возраст самого старого пакета
  * Пакеты  кроме ```waiting``` старше месяца удаляются


# Использование данных
Данные используются сервисом редактора НК для предоставления в UI информации об имеющихся фотографиях для POI.

Метод ```GET /tools/business-photos/$``` возвращает список зарегистрированных для ```permalink_id``` фотографий.

Сами фотографии также отображаются сервисом MRC через точки съёмки на подложке.
