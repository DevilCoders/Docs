# Перещелкивание vlan в RackTables

Для того, чтобы поменять vlan у железного сервера в racktables, необходимо:

1. В [eine.yandex-team.ru](https://eine.yandex-team.ru/) в поиске по серверам найти необходимый хост и перейти на его страницу.
2. На странице хоста найти графу `Switch/port` и перейти по ссылке в ней в racktables.

    ![image](images/check-port-eine.jpg)

3. На странице в racktables будет подсвечен нужный switch.

    ![image](images/shown-switch-rt.jpg)

4. В списке для этого свитча выбираем необходимый макрос. Для тестинга - `_VERTISDEVNETS_`, для прода - `_VERTISPRODNETS_`.

    ![image](images/choose-macros-rt.jpg)

5. В нижней части страницы сохраняем конфигурацию, нажимая на левую кнопку.

    ![image](images/save-vlan-rt.jpg)

6. Конфигурация синхронизируется в течение 10 минут.
