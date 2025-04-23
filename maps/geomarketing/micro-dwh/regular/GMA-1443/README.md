# [GMA-1443](https://st.yandex-team.ru/GMA-1443) Аудитории активных пользователей

### Периодичность сбора:
Каждый день

### Результаты:
Все таблицы расположены в директории [//home/maps/marketing/smb/micro-dwh/regular/GMA-1443/](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/marketing/smb/micro-dwh/regular/GMA-1443)
* **[segment_1_first_active_campaign](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/marketing/smb/micro-dwh/regular/GMA-1443/segment_1_first_active_campaign)** -
сегмент 1: оплатили первую РК за последние 90 дней и по ней есть открутки на вчера;
* **[segment_2_active_campaign](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/marketing/smb/micro-dwh/regular/GMA-1443/segment_2_active_campaign)** -
сегмент 2: имеют открутки на вчера, но РК не первая или первая, но создана более 90 дней назад;
* **[segment_3_not_active_first_campaign](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/marketing/smb/micro-dwh/regular/GMA-1443/segment_3_not_active_first_campaign)** -
сегмент 3: была создана и оплачена первая РК, но последняя открутка была более 30 дней назад;
* **[segment_4_not_active_campaign](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/marketing/smb/micro-dwh/regular/GMA-1443/segment_4_not_active_campaign)** -
сегмент 4: Были оплаченные РК (не первые), но последняя открутка была более 30 дней назад.

### Описание полей:
| **Название**           | **Описание**                                |
|------------------------|---------------------------------------------|
| update_date            | Дата обновления таблицы                     |
| bc_first_spending_date | Дата первой открутки балансового клиента    |
| bc_last_spending_date  | Дата последней открутки балансового клиента |
| bc_first_campaign_id   | Id первой кампании балансового клиента      |
| bc_last_campaign_id    | ID последней кампании балансового клиента   |
| yandex_puid            | Паспортный id Яндекса                       |
| crypta_gaid            | gaid из Крипты                              |
| crypta_yandexuid       | yuid из Крипты                              |
| crypta_idfa            | idfa из Крипты                              |
| tycoon_email_sha256    | Хеш email-а из Справочника                  |
| geoadv_email_sha256    | Хеш email-а из Яндекс Бизнес                |
| crypta_email_sha256    | Хеш email-а из Крипты                       |
| tycoon_phone_sha256    | Хеш номера телефона из Справочника          |
| geoadv_phone_sha256    | Хеш номера телефона из Яндекс Бизнес        |
| crypta_phone_sha256    | Хеш номера телефона из Крипты               |

### Особенности:
- Балансовый клиент - это balance_client_id из Яндекс Бизнес.
- Открутки считаются не по отдельной РК, а по всем РК балансового клиента,
т.е проверяется активность клиента, а не кампании.
- Забираем только тех клиентов, у которых есть хоть один из трёх хешей email-ов и телефонов.
