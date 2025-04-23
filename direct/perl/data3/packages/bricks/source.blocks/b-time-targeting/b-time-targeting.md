#Блок временного таргетинга

Контрол настройки коэффициентов ставок РК для конкретных временных периодов  

##Внешнее API:

###Параметры контекста params:

timeZoneGroups, // группы часовых поясов (Россия, СНГ, мир и т.д.) 
isExtendModeAvailable, // доступен ли расширенный режим 
value: {
    isExtendModeOn, // включен ли расширенный режим
    timeZone: {
        id, // идентификатор тайм зоны 
        text // текст тайм зоны  
    },
    timeTargetCode, // закодированная строка со ставками   
    isHolidaySettingsEnabled, // флаг "учитывать праздничные дни" (сейчас time_target_holiday)
    isWorkingWeekendEnabled, // флаг "учитывать рабочие выходные" (сейчас time_target_working_holiday) 
    holidayShowSettings: {   // необязательное поле        
        isShowing, // флаг "показывать на праздничных днях" (сейчас обратное time_target_holiday_dont_show)
        showingFrom, 
        showingTo,
        coefficient
    },
    preset // набор выбранных значений (все, рабочее время, другое) значения all, worktime, other
}

###Публичные методы:
getValue - возвращает текущее выбранное состояние формы таймтаргетинга
isValid - возвращает состояние валидности
setExtendModeAvailable – устанавливает доступность расширенного режима настроек (определён в модификаторе)
fixChanges – фиксирует изменение текущих настроек        
isChanged - Возвращает флаг наличия изменений в промисе
isChangedBoolean - возвращает флаг наличия изменений
cancel – отменяет изменение

##Модификаторы
###preset
модификатор который говорит про то, какой контрол (набор контролов) используется
####other
таблица
####worktime
селекты
определён на уровне Директа, для Лёгкого Интерфейса

##Пример использования блока 
{
    block: 'b-time-targeting',
    params: {
        timeZoneGroups: JSON.parse('[{"name":"Россия","timezones":[{"name":"Калининград (MSK -01:00)","group_nick":"russia","msk_offset":"-01:00","offset_str":"(MSK -01:00)","gmt_offset":"+02:00","timezone":"Europe/Kaliningrad","id":"131","country_id":"225","offset":7200,"timezone_id":"131"}]}]')        
        isExtendModeAvailable: true,
        value: {
            isExtendModeOn: false,
            timeZone: {
                id: '130',
                text: 'Москва'
            },
            timeTargetCode: '1IJKLMNOPQRST2IJKLMNOPQRST3IJKLMNOPQRST4IJKLMNOPQRST5IJKLMNOPQRST67',
            isHolidaySettingsEnabled: false,
            isWorkingWeekendEnabled: true,
            holidayShowSettings: {
                isShowing: false,
                showingFrom: undefined,
                showingTo: undefined,
                coefficient: 100
            },
            preset: 'other'
        }
    }
}

##Мысли по поводу рефакторинга:
1) В __prepare-data готовить только данные, без bemjson
2) Вложенные блоки реализовывать по концепции "черного ящика" (сейчас логика вложенных блоков частично реализована в базовом)
3) Изменить логику установки расширенного режим (см TODO)
4) В ViewModel использовать такой же нейминг и структуру, как во входных/выходных параметрах
5) Известаная проблема: при вызове getValue() модель становится измененной, т.к. в этом методе рассчитывается timeTargetingCode
Необходимо претащить этот расчет в модель и вызывать его динамически через calculate
6) Поддержать в блоке возможность установить значение настроек извне, для того, чтобы каждый раз не перешаблонизировать блок
при изменении входных данных
7) Удалить старую тему в b-time-targeting-scale и сделать _type_slider дефолтным (основая тема нигде не используется) 
