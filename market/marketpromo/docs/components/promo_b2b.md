# Работа с промо в ПИ

Общая архитектура promo b2b
![image](https://arcanum.yandex-team.ru/api/v1/repos/arc_vcs/tree/blob/junk/eandreyf/drawio/Promoprocess-mbi.drawio.png?commit_id=trunk)

## Особенности требований
1. Проверка заливки акционного ассортимента
Проверяем через saas каждый 1000 офер
2. Не ждём, когда весь потенциальный ассортимент доехал, показываем сразу как что-то есть
3. Сам контролируют очищение акционного ассортимента для акций из ПИ
4. Для партнёрских акций. Потенциальный ассортимент = все товары партнёра
5. Для истории акций храним только количество оферов партнёра в каждой акции. Вычисляем из генлога, храним внутри mbi

## Дополнительная документация
https://wiki.yandex-team.ru/non-adv-promotion/promokody-ot-partnerov-na-marketplejjse/

https://wiki.yandex-team.ru/users/akustareva/Kalendar-promo-dlja-postavshhikov-v-PI/
