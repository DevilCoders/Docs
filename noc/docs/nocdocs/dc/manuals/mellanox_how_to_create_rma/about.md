## Mellanox how to create the RMA

Автор: [Роман Глебов](https://staff.yandex-team.ru/kitaro)

Чтобы создать RMA у Mellanox, сначала нужно зарегистрироваться на их сайте support.mellanox.com Для регистрации нужно использовать корпоративную почту (вроде бы ни у кого проблем с регистрацией не было).Наиболее частой причиной RMA на сегодняшний день является износ SSD у SN2100 (проверка /dev/sda: Health 4.967 lower threshold 5). Примерный workflow для такого типа RMA выглядит следующим образом:
1. Перед созданием RMA со свитча нужно снять выводы следующих команд: 
  - `sudo smartctl -a /dev/sda`
  - `sudo iSMART_64 -d /dev/sda` 
  - и положить выхлоп в файлик.
2. Создаем RMA на сайте по образу и подобию с вот этим [RMA Acknowledgment Letter 122](https://jing.yandex-team.ru/files/vdvolovik/RMA_Acknowledgment_letter_929562.pdf). Нужно только подставить правильный серийник и в поле с диагностикой прикрепить файлик с выводами команд из пункта 1. При условии что коммутатор находится в SAS или VLA, для MAN реквизиты доставки и контактное лицо будут другими.
3. Далее через 1-2 дня вендор пришлет RMA Acnowledgment letter. После этого создаем тикет в startrack очередь RMA и приложить это письмо к тикету.
4. Перед отправкой по RMA свитч нужно сбросить в дефолт, сейчас мы это делаем переустановкой Cumulus. 
   - из Cumulus: onie-install -fa -i [http://93.158.158.93/tftpboot/cumulus/cumulus-linux-3.7.2-mlx-amd64.bin](http://93.158.158.93/tftpboot/cumulus/cumulus-linux-3.7.2-mlx-amd64.bin)
   - из ONIE: onie-nos-install [http://2a02:6b8:b010:31::100/tftpboot/cumulus/cumulus-linux-3.7.2-mlx-amd64.bin](http://2a02:6b8:b010:31::100/tftpboot/cumulus/cumulus-linux-3.7.2-mlx-amd64.bin)
   
   > **NOTE**
   >
   > Процедура занимает минут 15, после окончание на консоле появится приглашение в чистый cumulus. Сбрасывать можно либо перед заменой, либо после замены просить куда-то подключить менеджмент и консоль.
