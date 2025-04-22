##Графики и мониторинги

####Используемые системы
[Yasm](https://wiki.yandex-team.ru/jandekspoisk/sepe/golovan/) - графики по параметрам, получаемым из Qloud
[Juggler](https://wiki.yandex-team.ru/sm/juggler/) - система мониторинга

####Yandex
[Графики](https://yasm.yandex-team.ru/panel/_zUDaAw)
[Мониторинги](https://juggler.yandex-team.ru/?view=tiles&query=h%40%20%20%5B%20workspace.portal.prod%20%5D)
####Yandex-team
[Графики](https://yasm.yandex-team.ru/panel/_V5d5Ji)
[Мониторинги](https://juggler.yandex-team.ru/?view=tiles&query=h%40%20%20%5B%20workspace.portal-yandex-team.prod%20%5D)

####Описание как настроить получение нотификаций от juggler В Telegram
[Подробное описание на вики страничке Powny](https://wiki.yandex-team.ru/sm/powny/user/#telegram)    
Если вкратце:    
1. добавляем телеграмовский логин на стаф   
2. идем в [powny](https://powny.yandex-team.ru/juggler)   
3. кликаем в "добавить новое правило"   
4. в разделе "Host in:" указываем окружения о которых мы хотим получать нотификации(для коннекта это - workspace.portal.prod, workspace.portal-yandex-team.prod)   
5. кликаем в добавить оповещение, выбираем "в Телеграм", далеее забиваем свой логин со стафа и кликаем "Сохранить". Правило создано.    
6. добавляем себе в телеграм бота "powny_bot", потом в чате с ним пишем /star затем /subscribe    


