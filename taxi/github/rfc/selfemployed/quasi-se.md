# Квази-самозанятые

* пСМЗ -- полноценные СМЗ с собственным парком и зароботком
* кСМЗ -- квази СМЗ, обычные парковые подрядчики, репортящие доход в ФНС как СМЗ

## Задача
Дать возможность паркам репортить доходы подрядчиков как доходы за самозанятость

https://st.yandex-team.ru/TAXIMETERBACK-12186


## Существующая модель
%%(plantuml)
@startuml
!define table(x) class x << (T,#FFAAAA) >>
!define primary_key(x) <u><b>x</b></u>
!define key(x) <u>x</u>
hide methods
hide stereotypes

table(profiles) {
  primary_key(id[1])
  step
  status
  key(inn[2])
  key(from_park_id[3])
  key(from_driver_id[3])
  key(park_id[4])
  key(driver_id[4])
  ____
  personal data
}
@enduml
%%

*Рис 1. Таблица profiles.*

%%(plantuml)
@startuml
Tax->>SE++: /intro\n bind request
  SE->>pg.profiles: new prifile
SE->>Tax--: request accepted
note over Tax, FNS: Tax opens FNS app, driver registers in FNS
Tax->>SE++: /nalog-app\n fns registration complete
  SE->>FNS++: bind request
  FNS->>SE--: bind_request_id
  SE->>pg.profiles: bind_request_id
SE->>Tax--: ok
Tax->>SE++: agreement, address
  SE->>pg.profiles: agreement, address
SE->>Tax--: ok
note over Tax, FNS: Tax opens FNS app, driver gives permissions
Tax->>SE++: /permission\n permission given
  SE->>FNS++: get inn, fio
  FNS->>SE--: inn, fio
  SE->>pg.profiles++: mark fns bind complete, get agreement and address
  pg.profiles->>SE--: agreement, address
  SE->>ParCon: create new selfemployed park
SE->>Tax--: ok

ParCon->>SE++: /new-park-callback\n park created
  SE->>pg.profiles: park_id, driver_id
  SE->>Tax: (push) park created
SE->>ParCon--: ok
@enduml
%%
*Рис 2.1. Упрощённый флоу регистрации СМЗ*

<{Полный флоу регистрации
%%(plantuml)
@startuml
group Before any steps
  Tax->>SE++: /steps
  SE->>pg.profiles++: get current step by from_park_id, from_driver_id
  pg.profiles->>SE--: step
  opt step not found
    SE->>pg.profiles++: get profile by park_id, driver_id
    pg.profiles->>SE--: profile
    alt profile found
      SE->>Tax: only step is Requisities
    else no profile found
      SE->SE: take step as Intro
    end
  end
  SE->>Tax--: all steps and current step
end

group Step - Intro
  Tax->>SE++: /intro
    SE->>pg.profiles: new profile
  SE->>Tax--: next step - Nalog-App
end

group Step - Nalog-App
  note over Tax, FNS: Tax opens FNS app, driver registers in FNS

  Tax->>SE++: /nalog-app\n current phone
    SE->>FNS++: bind by phone (current phone)
    FNS->>SE--: bind_request_id
    alt driver used current phone to register in FNS
      SE->>pg.profiles: bind_request_id, current phone
      SE->>Tax: next step - Agreement
    else driver used another phone to register in FNS
      SE->>pg.profiles: current phone
      SE->>Tax--: next step - Phone-Number
    end
end

group Step - Phone-Number
  Tax->>SE++: /phone-number
    SE->>pg.profiles++: get last known phone
    pg.profiles->>SE--: last known phone
  SE->>Tax--: phone
  
  Tax->>SE++: /bind
  alt phone changed
    SE->>passport++: send sms
    passport->>SE--: sms_track_id
    SE->>pg.profiles: sms_track_id
    SE->>Tax: next step - SMS
  else
    SE->>FNS++: bind by phone (new phone)
    FNS->>SE--: bind_request_id
    SE->>pg.profiles: bind_request_id
    SE->>Tax--: next step - Agreement
  end
end

group Step - SMS
  Tax->>SE++: /confirm_phone\n sms code
  SE->>pg.profiles++: get phone, sms_track_id
  pg.profiles->>SE--: phone, sms_track_id
  SE->>passport++: check sms code
  passport->>SE--: check result
  alt check ok
  	SE->>Tax: next step - Phone-Number
  else
  	SE->>Tax--: try again
  end
end

group Step - Agreement
  Tax->>SE++: /agreement\n accepted agreement flags
  SE->>pg.profiles: accepted agreement flags
  SE->>Tax--: next step - Address
end

group Step - Address
  Tax->>SE++: /address\n driver address
  SE->>geocoder++: get postal code by address
  geocoder->>SE--: postal code
  SE->>pg.profiles: driver address and postal code
  SE->>Tax--: next step - Permission
end

group Step - Permission
  note over Tax, FNS: Tax opens FNS app, driver gives permissions
  
  Tax->>SE++: /permission
  SE->>pg.profiles++: get status, bind_request_id, phone, park_id
  alt status==REQUESTED
    pg.profiles->>SE--: bind_request_id
    SE->>FNS++: check bind status
    FNS->>SE--: inn
    alt bind success
      SE->>FNS++: get fio
      FNS->>SE--: fio
      SE->>pg.profiles: inn, fio
      SE->>ParCon: create park and driver
      SE->>Tax: next step - Requisites
    else bing incomplete
      SE->>Tax: try again
    else bind rejected
      SE->>FNS: bind by phone
      SE->>Tax: next step - Permission
    end
  else park_id is present
    SE->>Tax: next step - Requisities
  else
    SE->>Tax--: try again
  end
end

group Step - Requisities
  Tax->>SE++: /requisities
  SE->>pg.profiles: requisities
  SE->>ParCon: requisities
  alt requested from park profile
    SE->>Tax: next step - Finish
  else requested from se profile
    SE->>Tax--: next step - Exit
  end
end

group New Park Callback
  ParCon->>SE++: /new-park-callback\n new park created
    SE->>pg.profiles: park_id, driver_id
    SE->>Tax: (push) park created
  SE->>ParCon--: ok
end
@enduml
%%

*Рис 2.2. Флоу регистрации СМЗ*

}>

%%(plantuml)
@startuml
billing->>taximeter_back++: /process-events\n income data
taximeter_back->>dbparks.parks++: get park data
dbparks.parks->>taximeter_back--: park data
opt park is selfemployed
  taximeter_back->>SE++: /add-order[subvention]\n income data
  SE->>pg.profiles++: get inn
  pg.profiles->>SE--: inn
  SE->>pg.receipts: income data
  SE->>taximeter_back--: ok
end
taximeter_back->>billing--: ok
@enduml
%%
*Рис 3. Поступление чеков в сервис SE*

%%(plantuml)
@startuml
participant SE
participant pg.profiles
participant pg.receipts
participant FNS
loop
  SE->>pg.receipts++: get unsent receipt
  pg.receipts->>SE--: unsent receipt
  SE->>FNS++: add income
  FNS->>SE--: receipt id, receipt url
  SE->>pg.receipts: receipt id, receipt url
  opt taxpayer unbound
  SE->>pg.profiles: mark taxpayer unbound
  end
end
@enduml
%%

*Рис 4. Отправка чеков в ФНС*

Заметки:
1. Флоу инициируется из таксометра (для саморегов и парковых СМЗ),
   водитель пошагово заполняет форму регистрации СМЗ парка по ключу текущего профиля [3]
1. Через сервис `partner-contracts` создаётся новый парк и профиль водителя и их идентификаторы [4] сохраняются по ключу [1]
1. Чеки отправляются в сервис `selfemployed` по соответствующему признаку парка в `dbparks.parks`,
   по ключу [4] выбирается ИНН [2] самозанятого,
   данные чека и водителя сохраняются в шардированную таблицу receipts и ожидают отправки в ФНС
1. Крона `receipt_sync` обходит таблицу `receipts` и отправляет чеки в ФНС по ИНН [2]

### Недостатки существующей модели
1. Текущая модель данных рассчитана на полноценную форму регистрации с множеством полей, ненужных кСМЗ
1. К сожалению, в существующей модели невозможно сохранить 2 профиля СМЗ с одним ИНН,
   а это не позволит водителю иметь профиль пСМЗ и\или несколько профилей кСМЗ
1. В текущей модели проблематично добавить возможность передавать чеки в сервис самозанятых,
   т.к. придётся добавить признак самозанятости в профиль водителя `dbdrivers.drivers`


## Предлагаемая модель

%%(plantuml)
@startuml
!define table(x) class x << (T,#FFAAAA) >>
!define primary_key(x) <u><b>x</b></u>
!define key(x) <u>x</u>
hide methods
hide stereotypes


table(full_profile_initiators) {
    primary_key(from_db_id)
    primary_key(from_contractor_id)
    phone_pd_id
}


together {
  table(full_profile_forms) {
    primary_key(phone_pd_id)
    step
    resulting_db_id
    resulting_contractor_id
    ____
    personal data
  }

  table(quasi_profile_forms){
    primary_key(db_id)
    primary_key(contractor_id)
    phone_pd_id
  }
}

table(finished_profiles) {
  primary_key(db_id)
  primary_key(contractor_id)
  phone_pd_id
  do_send_receipts
  shard_number
}

table(nalogru_bonds) {
  primary_key(phone_pd_id)
  bind_request_id
  inn
  status
}

full_profile_forms *-- full_profile_initiators
nalogru_bonds *-[dashed]- full_profile_forms
nalogru_bonds *-[dashed]- quasi_profile_forms
nalogru_bonds *-- finished_profiles

finished_profiles <-[dashed]- quasi_profile_forms
finished_profiles <-[dashed]- full_profile_forms
@enduml
%%

*Рис 5. Предлагаемая модель данных*

В рамках предлагаемой модели появятся более гранулярные таблицы
* `nalogru_bonds` - строка таблицы описывает связь подрядчика MLU и ФНС. Первичный ключ такой свзязи - телефон (ПД Id)
* `finished_profiles` - строка таблицы описывает подрядчиков, согласившихся подавать информацию о своих доходах как СМЗ
* `full_profile_forms` - строка таблицы содержит форму регистрации пСМЗ. Поскольку один подрядчик может прийти в сервис из разных профилей - первичный ключ должен описывать самого подрядчика, и быть более стабильным чем unique_driver_id, так что я остановился на телефоне
* `full_profile_initiators` - вспомогательная таблица для поиска заполняемого профиля в `full_profile_forms` по db_id+contractor_id
* `quasi_profile_forms` - строка таблицы описывает запрос парка на подключение водителя как кСМЗ, принятые парком и водителем оферты, и вспомогательные данные, например id запроса к пасспорту для проверки телефона при смене

%%(plantuml)
@startuml
Tax->>SE++: /intro
  SE->>pg.full_profile_forms: new prifile
SE->>Tax--: request accepted
note over Tax, FNS: Tax opens FNS app, driver registers in FNS
Tax->>SE++: /nalog-app\n fns registration complete
  SE->>FNS++: bind request
  FNS->>SE--: bind_request_id
  SE->>pg.nalogru_bonds: bind_request_id
SE->>Tax--: ok
Tax->>SE++: /agreement, /address
  SE->>pg.full_profile_forms: agreement, address
SE->>Tax--: ok
note over Tax, FNS: Tax opens FNS app, driver gives permissions
Tax->>SE++: /permission
  SE->>FNS++: get inn, fio
  FNS->>SE--: inn, fio
  SE->>pg.nalogru_bonds: mark fns bind complete
  SE->>pg.full_profile_forms++: get agreement and address
  pg.full_profile_forms->>SE--: agreement, address
  SE->>ParCon: create new selfemployed park
SE->>Tax--: ok

ParCon->>SE++: /new-park-callback\n park created
  SE->>pg.finished_profiles: park_id, driver_id
  SE->>Tax: (push) park created
SE->>ParCon--: ok
@enduml
%%
*Рис 6.1. Упрощённый предлагаемый флоу регистрации пСМЗ*

Флоу не притерпит принципиальных изменений, только данные регистранта будут складываться не в одну кучу, а в три.
Это позволит переиспользовать имеющееся состояние связки с ФНС при регистрации пСМЗ после кСМЗ, или переиспользовать начатую форму пСМЗ при перелогине водитлеля из другого парка.

<{Полный предлагаемый флоу регистрации
%%(plantuml)
@startuml
group Before any steps
  Tax->>SE++: /steps
  SE->>pg.full_profile_forms++: get current step by from_db_id, from_contractor_id
  pg.full_profile_forms->>SE--: step
  opt step not found
    SE->>pg.full_profile_forms++: get profile by db_id, contractor_id
    pg.full_profile_forms->>SE--: profile
    alt profile found
      SE->>Tax: only step is Requisities
    else no profile found
      SE->SE: take step as Intro
    end
  end
  SE->>Tax--: all steps and current step
end

group Step - Intro
  Tax->>SE++: /intro
    SE->>pg.full_profile_forms: new profile
  SE->>Tax--: next step - Nalog-App
end

group Step - Nalog-App
  note over Tax, FNS: Tax opens FNS app, driver registers in FNS

  Tax->>SE++: /nalog-app\n current phone
    SE->>pg.nalogru_bonds: check existing bind
    opt already bound
      SE->>Tax: next step - Agreement
    end
    SE->>FNS++: bind by phone (current phone)
    FNS->>SE--: bind_request_id
    alt driver used current phone to register in FNS
      SE->>pg.full_profile_forms: current phone
      SE->>pg.nalogru_bonds: bind_request_id, current phone
      SE->>Tax: next step - Agreement
    else driver used another phone to register in FNS
      SE->>pg.full_profile_forms: current phone
      SE->>Tax--: next step - Phone-Number
    end
end

group Step - Phone-Number
  Tax->>SE++: /phone-number
    SE->>pg.full_profile_forms++: get last known phone
    pg.full_profile_forms->>SE--: last known phone
  SE->>Tax--: phone
  
  Tax->>SE++: /bind
  alt phone changed
    SE->>passport++: send sms
    passport->>SE--: sms_track_id
    SE->>pg.full_profile_forms: sms_track_id
    SE->>Tax: next step - SMS
  else
    SE->>FNS++: bind by phone (new phone)
    FNS->>SE--: bind_request_id
    SE->>pg.nalogru_bonds: bind_request_id
    SE->>Tax--: next step - Agreement
  end
end

group Step - SMS
  Tax->>SE++: /confirm-phone\n sms code
  SE->>pg.full_profile_forms++: get phone, sms_track_id
  pg.full_profile_forms->>SE--: phone, sms_track_id
  SE->>passport++: check sms code
  passport->>SE--: check result
  alt check ok
  	SE->>Tax: next step - Phone-Number
  else
  	SE->>Tax--: try again
  end
end

group Step - Agreement
  Tax->>SE++: /accept-agreement\n accepted agreement flags
  SE->>pg.full_profile_forms: accepted agreement flags
  SE->>Tax--: next step - Address
end

group Step - Address
  Tax->>SE++: /address\n driver address
  SE->>geocoder++: get postal code by address
  geocoder->>SE--: postal code
  SE->>pg.full_profile_forms: driver address and postal code
  SE->>Tax--: next step - Permission
end

group Step - Permission
  note over Tax, FNS: Tax opens FNS app, driver gives permissions
  
  Tax->>SE++: /permission
  SE->>pg.nalogru_bonds++: get status, bind_request_id, phone
  pg.nalogru_bonds->>SE--: status, bind_request_id, phone
  alt status==REQUESTED
    SE->>FNS++: check bind status
    FNS->>SE--: inn
    alt bind success
      SE->>FNS++: get fio
      FNS->>SE--: fio
      SE->>pg.full_profile_forms: fio, inn
      SE->>ParCon: create park and driver
      SE->>Tax: next step - Requisites
    else bing incomplete
      SE->>Tax: try again
    else bind rejected
      SE->>FNS: bind by phone
      SE->>Tax: next step - Permission
    end
  else db_id is present
    SE->>Tax: next step - Requisities
  else
    SE->>Tax--: try again
  end
end

group Step - Requisities
  Tax->>SE++: /requisities
  SE->>pg.full_profile_forms: requisities
  SE->>ParCon: requisities
  alt requested from park profile
    SE->>Tax: next step - Finish
  else requested from se profile
    SE->>Tax--: next step - Exit
  end
end

group New Park Callback
  ParCon->>SE++: /new-park-callback\n new park created
  SE->>pg.full_profile_forms: db_id, contractor_id
  SE->>pg.finished_profiles: finished profile data
  SE->>Tax: (push) park created
  SE->>ParCon--: ok
end
@enduml
%%

*Рис 6.2. Предлагаемый флоу регистрации пСМЗ*
}>

%%(plantuml)
@startuml
note over Disp: dispatcher makes contractor download an FNS app and register
Disp->>SE++: /bind-contractor\n db_id, contractor_id, personal_phone
SE->>driver_profiles++: get driver phones
driver_profiles->>SE--: driver phones
SE->>pg.quasi_profile_forms: create new form
SE->>FNS++: bind by phone
FNS->>SE--: bind_request_id
SE->>pg.nalogru_bonds: phone, bind_request_id
opt phone changed
  SE->>passport++: send sms
  passport->>SE--: sms code
  SE->>pg.quasi_profile_forms: sms code
end
SE->>Tax: push accept terms [and verify sms]
SE->>Disp--: contractor push sent successfully
note over Tax, FNS: Tax opens FNS app, driver gives permissions
Tax->>SE++: /accept-park-terms\n terms, [sms code]
SE->>pg.quasi_profile_forms++: get form
pg.quasi_profile_forms->>SE--: form
opt phone changed
  SE->>passport++: check code
  passport->>SE--: check result
  opt code check failed
    SE->>Tax: try again
  end
end
SE->>pg.nalogru_bonds++: get bind_request_id
pg.nalogru_bonds->>SE--: bind_request_id
SE->>FNS++: check binding status
FNS->>SE--: inn
SE->>pg.nalogru_bonds: inn
SE->>pg.finished_profiles: new profile
SE->>Tax--: ok
@enduml
%%

*Рис 7. Предлагаемый флоу регистрации кСМЗ*

История получается такая:
1. Диспетчер открывает экран "Сделать водителя кСМЗ", видит на нем предупреждения от юристов и инструкцию о том, что водитель должен скачать "Мой налог" и зарегистрироваться в нём с *личным* номером телефона
1. Диспетчер вводит номер телефона с которым водитель зарегистрировался в ФНС и отправляет запрос на привязку
  Мы сохраняем такой запрос в таблицу `quasi_profile_forms`, отправляем запрос на привязку в ФНС и сохраняем id запроса ФНС в `nalogru_bounds` и отправляем водителю пуш с дальнейшими указаниями
  Если профиля в ФНС не нашлось - диспетчер видит ошибку и должен повторить запрос, возможно исправив телефон
1. Водитель получает пуш, открывающий экран "Вас хотят сделать кСМЗ." С кнопкой открыть "Мой налог" и просьбой дать разрешения, кнопкой "Далее". По кнопке "Далее" открывается экран, объясняющий водителю на что он соглашается, соответсвующими галочками, кнопкой "Подтвердить" и кнопкой "Отклонить".
  По кнопке "Подтвердить" на бек отправляется запрос на завершение привязки, мы получаем от ФНС ИНН, сохраняем его в `nalogru_bounds` и сохраняем завершённый профиль в `finished_profiles`.
  Если водитель не дал разрешения в ФНС - он получает ошибку и возвращается на предыдущий экран
1. Если телефон в профиле отличется от введённого диспетчером, то перед экраном "открыть мой налог" водитель видит экран "введите код из смс", который отправляется дальше, по кнопке "подтвердить"

%%(plantuml)
@startuml
billing->>taximeter_back++: /process-events\n income data
  taximeter_back->>SE++: /add-income\n income data
    SE->>pg.finished_profiles___nalogru_bounds++: get inn, shard
    pg.finished_profiles___nalogru_bounds->>SE--: inn, shard
    opt inn found
      SE->>pg.receipts: income data + inn
    end
  SE->>taximeter_back--: ok
taximeter_back->>billing--: ok
@enduml
%%
*Рис 8. Поступление чеков в сервис SE*

%%(plantuml)
@startuml
participant SE
participant pg.nalogru_bounds
participant pg.receipts
participant FNS
loop
  SE->>pg.receipts++: get unsent receipt
  pg.receipts->>SE--: unsent receipt
  SE->>FNS++: add income
  FNS->>SE--: receipt id, receipt url
  SE->>pg.receipts: receipt id, receipt url
  opt taxpayer unbound
  SE->>pg.nalogru_bounds: mark taxpayer unbound
  end
end
@enduml
%%

*Рис 9. Отправка чеков в ФНС*

**Заметки**:
1. Флоу, инициированные из диспетчерской и таксометра заполняют разные формы регистрации в разных таблицах, потому, что имеют разный набор необходимых данных и разный продуктовый смысл
1. Проверка необходимости передавать информацию о доходе внесена внутрь сервиса СМЗ, 
   т.к. признак в dbparks.parks теперь отвечает не на вопрос "является ли профиль СМЗ",
   а на опрос "является ли профиль пСМЗ"
1. Таблица с завершёнными профилями `finished_profiles` вынесена отдельно для того, чтобы при проверке из предыдущего пункта не искать СМЗ по отдельным таблицам полных и квази профилей
1. Таблица с привязками ФНС `nalogru_bounds` вынесена отдельно, чтобы обеспечить возможность одному СМЗ работать в нескольких парках не прибегая копированию статуса привязки по всем профилям
1. Таблица авторизации регистрирующегося `full_profile_initiators` пСМЗ вынесена отдельно для того, чтобы решить нашю давнюю боль с тем, что водителели создают несколько конфликтующих записей в таблице `profiles`
1. Флаг `do_send_receipts` необходим для п.1.4 тикета ("тумблер...") и недоступен для редактирования пСМЗ
1. Шард для сохранения чеков удобнее хранить прямо в таблице готовых профилей,
   решардинг от этого станет только проще, т.к. можно будет выполнять последовательно


## Шаги разработки бекенда

1. Добавить таблицы `nalogru_bounds`, `finished_profiles`, `quasi_profile_forms` (4h)
1. Добавить парковую ручку для инициации флоу кСМЗ `/bind-contractor` (рис. 7), только с явным указанием настоящего телефона СМЗ (8h)
1. Добавить парковую ручку для проверки статуса регистрации, привязки и состояния флага `do_send_receits` `/get-contractor-status` (8h)
1. Добавить парковую ручку для установки флага `do_send_receipts` `/activate-bound` (4h)
1. Добавить таксометровую ручку реакции на пуш (рис. 7) `/accept-park-terms` (16h)
1. В кроне `receipt_sync`, в случае ошибки от ФНС, обновлять статус профиля в таблице `nalogru_bounds`
   рядом с обновлением статуса в `profiles` (2h)
1. Добавить поле `do_send_receipt` в таблицу `receipts`, начальное значение - True
   Это будет необходимо, чтобы не терять чеки, заблокированные парком, 
   и иметь возможность проводить сверку с биллингом (4h)
1. Добавить обработчик всех событий от биллинга, выбирающий только нужные (рис 8) (24h)
1. Добавить возможность блокировать СМЗ
   1. Добавить ручку для выгрузки статусов СМЗ в `candidates` (8h)
   1. Добавить в `candidates` кеш признаков и фильтр, блокирующий водителей по условию
      `if bound_status!=OK and do_send_receipts` (40h)
1. **На этом этапе можно запускать фитчу**
1. Добавить в профиль водителя в tariff-editor признак кСМЗ и состояние регистрации (не работал с админкой, пусть будет 2d)
1. Перевести флоу регистрации пСМЗ на новые таблицы
   1. Начать писать в новые таблицы параллельно старой (3d)
   1. Перенести скриптом существующие профили в новую таблицу (3d)
   1. Начать читать из новых таблиц (2d)
   1. Закопать старый флоу (1d)
1. Добавить в tariff-editor раздел для наблюдения за статусом ФНС по телефону (не работал с админкой, пусть будет 5d)
1. Добавить возможность регистрировать кСМЗ без явного указания телефона диспетчером, со сменой на таксметре (5d)


## Дополнительно
### Альтернативное предложение по реализации
%%(plantuml)
@startuml
!define table(x) class x << (T,#FFAAAA) >>
!define primary_key(x) <u><b>x</b></u>
!define key(x) <u>x</u>
hide methods
hide stereotypes

table(quasi_profiles) {
  primary_key(park_id)
  primary_key(driver_id)
  key(profile_id[1])
  do_send_receipts
}

table(profiles) {
  primary_key(id[1])
  step
  status
  key(inn)
  key(from_park_id)
  key(from_driver_id)
  key(park_id)
  key(driver_id)
  ____
  personal data
}

quasi_profiles --* profiles
@enduml
%%
В качестве альтернативного предложения предлагалось рассмотреть модель, при которой кСМЗ профили цепляются за существующие пСМЗ

Плюсы:
* Выглядит не так страшно
* Возможно быстрее реализовать (см. далее)

Минусы:
* У подрядчика может не быть профиля пСМЗ, а, значит, придется рассмотреть один из двух костылей:
  * Заставить кСМЗ сначала регистрировать пСМЗ профиль
    * Это сложно для пользователя и заметно уменьшит кол-во желающих воспользоваться фитчей
  * Изменить модель данных таблицы `profiles`:
     * Это не сильно уменьшит время изначального внедрения решения относительно разработки новой модели рядом с существующей
     * Если фитча по какой-то причине не взлетит изменения будет сложнее откатывать
     * Вместо разрешения существующего техно долга мы добавим еще больше нового
* На каждый создаваемый чек придётся перебирать 2 таблицы: сначала поискать исполнителя как пСМЗ, а потом как кСМЗ - это может привести к проблемам с производительностью, особенно при пиковых нагрузках
