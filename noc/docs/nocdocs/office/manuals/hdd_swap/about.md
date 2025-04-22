FreeBSD
# 0.Узнаем серийник

- smartctl -a /dev/da1
# 1.Смотрим разметку диска

- gpart show -l  
  ```
  =>        34  1953525101  da0  GPT  (931G)
         34           6       - free -  (3.0k)
         40         128    1  boot1  (64k)
        168    83886080    2  swap1  (40G)
   83886248   188743680    3  root1  (90G)
  272629928  1680895207       - free -  (801G)
  
   =>        34  1953525101  da1  GPT  (931G)
         34           6       - free -  (3.0k)
         40         128    1  boot0  (64k)
        168    83886080    2  swap0  (40G)
   83886248   188743680    3  root0  (90G)
  272629928  1680895207       - free -  (801G)
  ```
# 2.Отключаем swap сбойного диска

- ```
  swapinfo                                                                                                                                                                                                      
   Device          1K-blocks     Used    Avail Capacity
   /dev/gpt/swap0   41943040        0 41943040     0%
   /dev/gpt/swap1   41943040        0 41943040     0%
   Total            83886080        0 83886080     0%
  ```
**Если сбойный диск был в составе свопа и его физически заменили без выключения сервера, то для дальнейших действий над новым диском машину нужно перезагрузить. При этом нужно убедиться, что машина будет загружаться с диска, который не меняли (на случай если замена была не на новый диск).**Это нужно по следующей причине. Т.к. диск был в свопе, система "удерживает" его и GEOM не может создать новый диск с тем же именем. Обычно это видно по ошибкам в консоли во время замены диска. Кажется в 11-ой версии эта проблема уже не актуальна, но нужно проверять.
- root@fol2-fw3 ~
  $ swapoff /dev/gpt/swap0
# 3.Выводим диск из рейда

- ```
  zpool status
    
      pool: zroot
   state: ONLINE
    scan: resilvered 118K in 0h0m with 0 errors on Wed May 27 15:05:51 2015
  config:
  
  	NAME           STATE     READ WRITE CKSUM
  	zroot          ONLINE       0     0     0
  	  mirror-0     ONLINE       0     0     0
  	    gpt/root0  ONLINE       0     0     7
  	    gpt/root1  ONLINE       0     0     0
  ```
- zpool detach zroot gpt/root0
# 4. SSD: Стираем содержимое

Стирать будем методом выдачи команды TRIM на весь объем SSD`newfs -E -t -b 64k -f 64k -i 64M /dev/da1`
# 5.После замены диска, делаем разметку на новом

- Для SSD дисков нужно зачистить диск перед созданием новой файловой системы с помощью утилиты newfs: 
  newfs -E -t -b 64k -f 64k -i 64M /dev/da1
  . Это запустит команду TRIM, фактически разблокирует для записи "грязные" сектора.
- gpart destroy -F da1
   (Нужно, только если диск с разметкой)//Если отдает gpart: Device busy , скорее всего нужна перезагрузка, т.к. проблема со свопом //
- gpart create -s GPT da1
- gpart add -a 4k -s 512k -t freebsd-boot -l boot0 da1
  цифра в boot0 (и далее swap и root) уникальна для каждого диска, смотрим имеющиеся и берем свободные, т.е. у одного диска цифры одинаковые (boot0, root0, swap0)
- gpart bootcode -b /boot/pmbr -p /boot/gptzfsboot -i 1 da1
  здесь -i это индекc (третий столбец gpart show -l), т.к. нам нужен загрузочный раздел, а он у нас первый здесь всегда 1
- gpart add -a 4k -s 40G -t freebsd-swap -l swap0 da1
- gpart add -a 4k -s 90G -t freebsd-zfs -l root0 da1
# 6.Добавляем новый размеченный диск в рейд

- zpool attach zroot /dev/gpt/root1 /dev/gpt/root0эта магия работает как zpool attach POOL PRESENT_DEVICE NEW_DEVICE, т.е. к любому уже существующему в зеркале разделу цепляем новый
# 7.Включаем swap

- swapon /dev/gpt/swap0