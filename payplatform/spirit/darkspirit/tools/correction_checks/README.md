# Пробитие чеков коррекции

Общая схема:
 - в динамической табличке описываются "задачи" на пробитие чеков коррекции,
    * MissingDocumentCorrectionTask - если чек по платежу не был выбит. [Пример](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/balance/prod/spirit/correction_checks/SPIRIT_1633/check) (нужно заполнить `transaction_id`, `correction_receipt` и `inn`)
    * ReceiptRollbackCorrectionTask - если чек был выбит, но его нужно "отменить". [Пример](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/balance/prod/spirit/correction_checks/check) (нужно заполнить только id исходного документа в даркспирите - `ds_doc_id`, ИНН ЮЛ и содержание чека корреции будут сформированы через ручку DS),
    * `correction_state` и `correction_doc` изначально пустые, их заполнит скрипт пробития чеков.
 - проверяется наличие достаточного количество касс для всех ЮЛ+группа по которым надо бить чеки (про группы смотри ниже),  
 - настраивается под конкретную задачу и запускается `run_correction.py`: скрипт берет задачки c `correction_state=null` из таблицы батчами, пытается пробить соответствующие чеки и записывает результат  в `correction_state` ("успех/не успех") и `correction_doc` ,
 - выполняется сверка наших данных с данными ОФД. [Примерный алгоритм](https://st.yandex-team.ru/SPIRIT-1603#5fda43940d04cf4043d833b0).

Для пробития чеков есть возможность использовать кассы определенной группы. Сейчас в скрипте зашита CORRECTION, но при необходимости можно указать что-то ещё или вообще не выбирать - тогда будут выбираться любые живые кассы.
Лучше если касс будет не меньше чем воркеров в скрипте. А в идеале на них ещё не должно литься другой нагрузки (в т.ч. в них не должны лететь обычные чеки). 
В противном случае высока вероятность огрести много ошибок при пробитии чеков и потратить много времени на сверку с ОФД.

`utils.py` - всякие вспомогательные команды для работы с табличкой в yt, 