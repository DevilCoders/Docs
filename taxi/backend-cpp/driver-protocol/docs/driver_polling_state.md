## Поллинг
URL `/driver/polling/state`

### Параметры

- `db` - идентификатор парка
- `session` - водительская сессия для проверки авторизации
- `license_verification` - флаг, показывающий нужно ли идти в монгу за актуальными данными о поле license_verification для водителя. Опциональный, true/false. Отсутствие означает false.

Заголовки ответа:
`X-Polling-Delay`: <период с секундах, через который приложение должно повторить запрос>

Значение периода задается в конфиге

    {
      "TAXIMETER_POLLING_DELAYS":
      {
        ...
        "/driver/polling/state" : 300
        ...
      },
    }

Ответ содержит 4 основных элемента.

- `gps_params` 
- `profile`
- `taximeter_configs`

### gps_params

TODO: сделать описание, введено в рамках тикета https://st.yandex-team.ru/TAXIBACKEND-11402

### profile
 
Добавлено в рамках задачи https://st.yandex-team.ru/TAXIBACKEND-12451. Присутствует в ответе, только если включен 
эксперимент по водителя `silver_crown`. Если у водителя 8ой грейд во всех тарифах в `dbtaxi.class`, которые есть в 
городе его парка и не отключены грейдами, тогда это поле возвращается и имеет значение `silver_crown`, иначе отсутствует.
Если пересечённый список тарифов водителя равен нулю - поле также отсутствует.

### weariness

Информации об усталости водителя. Описано в https://st.yandex-team.ru/TAXIBACKEND-13013#1526315978000. Включается по эксперименту "driver_weariness" по водителям.

### tutorial_config

Информации по туториалу обучения водителя. Присутствует, если эта настройка включена в настройках dbtaxi.countries для 
водителя. Подробное описание параметров в тикете: https://st.yandex-team.ru/TAXIBACKEND-15441 .

Пример ответа:

      "tutorial_config": {
        "fallback_to_web": false,
        "mode": "none",
        "reason": "config",
        "show_in_settings": true,
        "web_tutorial_url": "test_web_tutorial_url"
      }

### taximeter_configs

Пример ответа:

    {
      taximeter_configs : {
        anti_surge_params : {
          detect_delay_seconds : 3,
          max_speed : 20,
          recalc_delay_seconds : 60,
          show_in_busy : true
        },
        balance : -7760.285613,
        battery_optimization_params : {
          delay_to_process_seconds : 30,
          enabled : true,
          loop_frequency_seconds : 10
        }
        car_chairs_params : {
          booster_count : 0,
          chair_count : 2,
          chairs : [
            {
              "brand": "ABC Design",
              "categories": [1, 2, 3],
              "isofix": false
            },
            {
              "brand": "Yandex"
            }
          ]
        },
        car_services : ["wifi", "animals"],
        driver_client_chat_params : {
          polling_delay_seconds : 50,
          speechkit_inactivity_timeout_seconds : 15,
          startup_delay_seconds : 60
          bubble_visible_timeout : 20
          bubble_visible_timeout_after_speech : 15
          recognizer : "yandex_speechkit"
          vocalizer : "undefined",
          language_code : "ru_RU"
        },
        driving_params : {
          map_activation_distance : 432.5,
          open_navi_delay_ms : 1000,
          update_navi_passengers_millis : 10000,
          meters_delta_to_passenger : 600.0,
          outdated_passenger_delta_millis : 120000
        },
        finance_params : {
          can_pay_in : false
        },
        fixed_price_params : {
          receipt_show_meters : true,
          ui_show_meters : true
        },
        gps_params : {
          "0": 2,
          "25": 10,
          "90": 10
        },
        limit : 0,
        onlycard : false,
        paid_waiting_params : {
          enable : true,
          radius_to_turn_off : 501,
          speed_to_turn_off : 5
        },
        qc_params : {
          dkk_date : "2018-02-17T08:58:00.000000Z",
          dkb_chair_date : "2100-01-01T00:00:00.000000Z",
          dkb_chair_file : "www.youtube.com/watch?v=jHst7krrDdo",
          dkvu_check : false,
          hide : false,
          hours_to_deadline : 72,
          ready : false,
          selfie_check : false,
          menu_text : "Фотоконтроль",
          state_text : "Следующая проверка 14.02.2018. Вы сможете пройти её за 6 ч. до срока в любое удобное время",
          without_bso : false
        },
        uber_params : {
          backend_enabled : true,
          integration_enabled : true,
          rush_hours : [
            {
                'start': 3,
                'end': 4
            },
            {
                'start': 0,
                'end': 23
            }
          ],
          rush_hours_enable : true,
          rush_hours_start_delay_ms : 300000,
          status_change_restart_delay_ms : 1000,
          status_change_timeout_ms : 8000
        },
        version : "8.30",
        waiting_in_transporting_params : {
          enable : true,
          radius_to_turn_off : 50,
          seconds_to_show : 180,
          speed_to_hide : 10
        },
        waiting_params : {
          enable : true,
          max_order_distance : 500,
          max_order_distance_airport : 500,
          max_order_distance_linear : 40,
          max_order_pedestrian_distance : 100,
          max_order_pedestrian_distance_airport : 100,
          max_phone_call_distance : 500,
          max_phone_call_distance_airport : 1500,
          max_phone_call_distance_linear : 100,
          max_speed : 10,
          response_timeout : 5,
          route_timeout_ms : 30001
        },
        work_shifts_enabled : true,
        gas_stations_consent_accepted: true
      },
      positioning_mode: {
        enabled: true,
        mode: home,
        point: [60, 30]
      }
    }

`anti_surge_params` - настройки для водителя в зоне антисуржа
- `detect_delay_sec` - частота в секундах, с которой проверяется, находится водитель в антисурж зоне (uint)
- `max_speed` - максимально допустимая скорость водителя при которой показывается антисурж нотификация (uint)
- `recalc_delay_seconds` - частота хождения за суржом для расчета (uint)
- `show_in_busy` - показывать нотификации об антисурже водителю когда он в статусе busy (true/false)

`balance` - баланс водителя (double)

`battery_optimization_params` - параметры оптимизации энергопотребления
- `delay_to_process_seconds` - период допустимой дупликации gps-координат (uint)
- `enabled` - включен ли режим (true/false)
- `loop_frequency_seconds` - частота опроса изменений gps-координат на предмет активности режима энергосбережения (uint)

`car_chairs_params` - параметр, описывающий детские кресла в машине водителя.
- `booster_count` - количество заявленных бустеров (uint)
- `chair_count` - количество детских кресел (uint)
- `chairs` - список кресел. Каждое кресло может иметь до 3 полей: `brand` (строка), `categories` (массив целых чисел), `isofix` (true или false)

`car_services` - услуги, возможные для данной машины. Массив строк.

`driver_client_chat_params` - настройки чата клиент-водитель
- `polling_delay_seconds` - время поллинга для чата в секундах (uint)
- `speechkit_inactivity_timeout_seconds` - время в секундах, через которое SpeechKit будет выключаться при неактивности (uint)
- `startup_delay_seconds` - Время в секундах, через которое чат с водителем будет запущен после начала заказа (uint)
- `bubble_visible_timeout` Таймаут закрытия бабла сообщения без озвучки
- `bubble_visible_timeout_after_speech` Таймаут закрытия бабла сообщения после озвучки
- `recognizer` тип speech-to-text. "undefined" если не используется
- `vocalizer` тип text-to-speech. "undefined" если не используется
- `language_code` код языка

`driving_params` - параметры перехода водителя в статус driving
- `map_activation_distance` - расстояние, показывающее  за сколько метров до подачи нужно показать карту (double)
- `open_navi_delay_ms` - задержка открытия навигатора в миллисекундах при переходе в статус driving (uint)
- `update_navi_passengers_millis` - интервал обновления навигатора (long int)
- `meters_delta_to_passenger` - дельта при подъезде к пассажиру на x метров (double)
- `outdated_passenger_delta_millis` - дельта устаревания данных пассажира в миллисекундах (long int)

`finance_params` - настройки доступности кошельков в платежных системах для пополнения счета
- `can_pay_in` - может ли водитель пополнить счет, используя кошелек или шлюз платежных систем (true/false)

`fixed_price_params` - параметры скрытия километража и времени
- `receipt_show_meters` - параметр для отображения в чеке (true/false)
- `ui_show_meters` - параметр для отображения на экране заказа (true/false)

`gps_params` - периоды передачи GPS-координат в зависимости от скорости движения. Список пар (uint, uint).

`limit` - лимит средств водителя (double)

`onlycard` - признак того, что можно делать только карточные заказы

`paid_waiting_params` - параметры выключения платного ожидания
- `enable` - включен ли режим (true/false)
- `radius_to_turn_off` - расстояние до точки подачи, при котором на Таксометре приостанавливается платное ожидание (в статусе waiting) (uint)
- `speed_to_turn_off` - cкорость, при которой на Таксометре приостанавливается платное ожидание (в статусе waiting) (uint)

`qc_params` - параметры для проверки контроля качества:
- `dkk_date` - дата водительского ДКК (date), опциональное (отсутствует если информация не была найдена)
- `dkk_not_required` - поле, показывающее, что ДКК не требуется, опциональное
- `dkb_chair_date` - дата проверки ДКБ детских кресел (date), опциональное (отсутствует если информация не была найдена)
- `dkb_chair_not_required` - поле, показывающее, что ДКБ не требуется, опциональное
- `dkb_chair_file` - URL видеоинструкции по ДКБ детских кресел (string)
- `dkvu_check` - признак того, что из всего ДКК надо проходить только ДКВУ (true/false)
- `hide` - скрывать ли кнопку "Пройти фотоконтроль" на экране КК (true/false)
- `hours_to_deadline` - количество часов до следующей проверки (uint)
- `ready` - готовность к прохождению контроля качества (меньше X часов до дедлайна) (true/false)
- `selfie_check` - признак того, что нужно проходить селфи контроль (true/false)
- `without_bso` - признак того, что бланк строгой отчетности не нужен (true - не нужен, false - нужен)
- `state_text` - текст на экране КК в таксометре (string)
- `menu_text` - текст на экране КК в таксометре (string)

`uber_params` - параметры для убера. Опциональное поле (отображается при включенном конфиге TAXIMETER_UBER_INTEGRATION_ENABLED).
- `backend_enabled` - включен ли бэкенд UBER для клиента Таксометра (true/false)
- `integration_enabled` - дата проверки ДКБ детских кресел (true/false)
- `rush_hours` - интервалы часов пик для запуска UBER Driver. Массив интервалов с полями start и end (0 - 23)
- `rush_hours_enable` - включена ли логика для запуска UBER Driver в часы пик (true/false)
- `rush_hours_start_delay_ms` - время в мс, в течение которого в клиенте Таксометре нет заказов, для запуска UBER Driver в часы пик (uint)
- `status_change_restart_delay_ms` - задержка рестарта клиента таксометра в мс при изменении статуса в UBER Driver через Accessibility (uint)
- `status_change_timeout_ms` - таймаут изменения статуса в мс в UBER Driver через Accessibility (uint)

`version` - Текущая версия таксометра

`waiting_in_transporting_params` - параметры включения/выключения ожидания в пути
- `enable` - включен ли режим (true/false)
- `radius_to_turn_off` - требуемое расстояние для включения режима ожидания в пути (uint)
- `seconds_to_show` - количество секунд с момента остановки до показа кнопки "Ожидание в пути" (uint)
- `speed_to_hide` - скорость в км/ч, при которой кнопка "Ожидание в пути" должна скрываться (uint)

`waiting_params` - параметры перехода в статус Waiting
- `enable` - включен ли режим (true/false)
- `max_order_distance` - расстояние в метрах до точки подачи, необходимое для перехода в статус waiting (uint)
- `max_order_distance_airport` - расстояние в метрах до точки подачи в зоне аэропорта (uint)
- `max_order_distance_linear` - максимально допустимая дистанция в метрах для расчёта "по прямой", на которой водителю позволяется отмечаться "на месте" без расчёта расстояния по карточному роутеру (uint)
- `max_order_pedestrian_distance` - пешее расстояние в метрах до точки подачи, необходимое для перехода в статус waiting (uint)
- `max_order_pedestrian_distance_airport` - пешее расстояние в метрах до точки подачи в зоне аэропорта (true/false)
- `max_phone_call_distance` - расстояние в метрах до точки подачи, требуемое  для того чтобы водитель мог позвонить клиенту (uint)
- `max_phone_call_distance_airport` - расстояние в метрах до точки подачи в зоне аэропорта, требуемое для того чтобы водитель мог позвонить клиенту (uint)
- `max_phone_call_distance_linear` - максимально допустимая дистанция в мерах для расчёта "по прямой" для звонка пассажиру, без расчёта расстояния по карточному роутеру (uint)
- `max_speed` - максимальная скорость в км/ч для перехода в статус waiting (uint)
- `response_timeout_ms` - таймаут запроса к бэкенду в секундах для подтверждения перехода в статус waiting (uint)
- `route_timeout_ms` - таймаут в мс запроса в driving router (uint)

`work_shifts_enabled` - признак того, что включена покупка смен

`gas_stations_consent_accepted` - Признак того, что парк водителя принял оферту Яндекс.Заправок (true/false)

`status` - Текущий статус водителя. Может принимать значения offline, free, busy

### Пример вызова ручки

`curl "driver-protocol.taxi.dev.yandex.net/driver/polling/state?db=c52e88b724674ef7917ee0f8fa4627de&session=abcd18cfb6ad465ab6f47a4d73f7d42c&license_verification=true"`
