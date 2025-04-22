# advisor-money
Денежные расчеты advisor

# запуск команд ручками
    $ source /opt/venvs/yandex-mobile-advisor-money/bin/activate
    $ MONEY_SETTINGS_MODULE=advisor_money.user_settings parse_postbacks_mongo

логи будут в каталоге: ~/tmp/var/log/yandex/advisor-money

по умолчанию, если не установлена переменная среды MONEY_SETTINGS_MODULE, то используется модуль settings

