# @yandex-taxi/cc-jssip-hooks

Пакет для работы с телефонией и бэкендом яндекс такси.

Использует под капотом jssip.

[События виджета](https://events.chv.yandex-team.ru/projects/callcenter_frontend_events/?componentSettings=%7B%22row_1_col_0_con_0_charts%22%3A%7B%22field%22%3A%22name%22%7D%7D)

## Установка

```
npm install @yandex-taxi/cc-jssip-hooks
```


## Документация

Как это работает?

Мы используем АПИ бэкенда в который ходим через cc-authproxy. Чтобы начать взаимодействие с телефонией нужно:
1) Быть зарегистрированным в системе КЦ. (Нужно чтобы получать токен с которым будем подключаться к серверам телефонии.)
   
Завести учетки можно здесь 
[Тестинг](https://tariff-editor.taxi.tst.yandex-team.ru/call-center/operators)
[Прод](https://tariff-editor.taxi.yandex-team.ru/call-center/operators)

2) Быть залогиненым через яндекс паспорт.

(Под капотом)

Библиотека обменивает куку пользователя на токен с которым подключается к серверам телефонии. А также прокидывает в приложение
множество полезных функций и состояний в КЦ.

### Локальное подключение пакета (dev режим)
В корне репозитория пакета
```
npm link
```

В проекте в котором используется пакет
```
npm link @yandex-taxi/cc-jssip-hooks
```

### Базовый пример

Демо тут:
https://phoneorderbeta.taxi.tst.yandex.ru/test

```
    ====index.tsx====
   
    import {server} from '@yandex-taxi/callcenter-staff/bunker';
    import CallcenterProvider from '@yandex-taxi/cc-jssip-hooks';
    import React from 'react';
    
    import config from './appConfig';
    import Test from './Test';
    
    // Компонент обертка
    const TestWrapper = () => (
        <CallcenterProvider
            host={server.authproxyHost}
            project={config.projectName}
            env={config.env}
            version={config.version}
        >
            <Test/>
        </CallcenterProvider>
    );
    
    export default TestWrapper;
    
    =====Test.tsx=====
    
    import {useCallcenterStatus, useSetCallcenterStatus} from '@yandex-taxi/cc-jssip-hooks/callcenter';

    // Компонент обертка
    const Test = () => {
        // Получаем состояние статуса
        const [{loading, data, error}, setStatus] = useTelephonyStatus();
        const {status: uaStatus} = useUserAgent();
        const {loading: hashLoading, data: hashData, error: hashError} = useTelephonyHash();
        const {loading: launchLoading, data: launchData, error: launchError} = useTelephonyLaunch();
        const {status: sessionStatus} = useSession();
    
        if (hashError || launchError) {
            return <div>Ошибка получения данных для подключения к серверам телефонии</div>;
        }
    
        if (hashLoading || !hashData || launchLoading || !launchData) {
            return <div>Загружаем данные</div>;
        }
    
        return (
            <div>
                <Row>
                    <h1>Тестирование библиотеки</h1>
                </Row>
                <Row>{`Ваш логин: ${launchData?.login}`}</Row>
                <Row>{`Ваш текущий статус в телефонии: ${data?.status}`}</Row>
                <Row>{`Ваш текущий статус на регистарах: ${uaStatus}`}</Row>
                <Row gap="s">
                    <Col gap="s">
                        <Button disabled={loading || data?.status === Status.CONNECTED} loading={loading} onClick={() => setStatus({status: Status.CONNECTED})}>
                            Выйти на линию
                        </Button>
                    </Col>
                    <Col gap="s">
                        <Button disabled={loading || data?.status === Status.DISCONNECTED} loading={loading} onClick={() => setStatus({status: Status.DISCONNECTED})}>
                            Уйти с линии
                        </Button>
                    </Col>
                </Row>
                {error && <Row>Ошибка статуса</Row>}
                {sessionStatus !== SessionStatus.WAITING && <Session/>}
            </div>
        );
    };
    
    export default Test;
    
    ======Session.tsx=======

    import {
        SessionDirection,
        SessionStatus,
        useAnswerCall,
        useEndCall,
        useSession,
        useSessionSelector,
    } from '@yandex-taxi/cc-jssip-hooks';

    const toProps = ({session}: RTCSessionEvent) => ({
        phone: session.remote_identity.uri.user,
        queue: session.remote_identity.display_name,
    });
    
    const ANSWER_CALL_OPTIONS: CallOptions = {
        mediaConstraints: {
            audio: true,
            video: false,
        },
        pcConfig: {
            iceServers: [
                {
                    urls: STUN_SERVERS // Можно задать свой стан сервер
                },
            ],
    },
    
    // Обработка звонка
    const Session = () => {
        const {
            status: sessionStatus,
            direction,
        } = useSession();
    
        const {
            phone,
            queue,
        } = useSessionSelector(toProps);
    
        const answerCall = useAnswerCall();
        const endCall = useEndCall();
    
        return (
            <>
                {sessionStatus === SessionStatus.STARTING && direction === SessionDirection.INCOMING && (
                    <>
                        <Row>Входящий вызов</Row>
                        <Row>{`Очередь: ${queue}`}</Row>
                        <Row>{`Номер: ${phone}`}</Row>
                        <Row>
                            <Button onClick={() => answerCall(ANSWER_CALL_OPTIONS)}>Ответить</Button>
                        </Row>
                    </>
                )}
                {sessionStatus === SessionStatus.ACTIVE && (
                    <>
                        <Row>Вы сейчас разговариваете</Row>
                        <Row>{`Очередь: ${queue}`}</Row>
                        <Row>{`Номер: ${phone}`}</Row>
                        <Row>
                            <Button onClick={() => endCall()}>
                                Закончить вызов
                            </Button>
                        </Row>
                    </>
                )}
            </>
        );
    };
```

### CallcenterProvider
Основной компонент телефонии.

```
interface Props {
    host: string; // Хост бэкенда для телефонии.
    onStatusChange?: (prevStatus: string, status: string) => void; // Колбэк если на бэкенде изменился статус агента.
    onSessionTerminate?: (data: TerminateOptions) => void; // Колбэк отбития вызова
    startSessionDisabledReason?: string; // Используется для отбития звонков, если абонент не может говорить в текущий момент
}
```

### Хуки ручек

#### useTelephonyHash - получение хэша для авторизации перед телефонией
```
    // Получаем состояние загрузки хэша
    const {loading, data, error} = useTelephonyHash();
    
    // Если не удалось получить можно вывести заглушку
    if (error) {
        return 'Нет данных для авторизации телефонии'
    }
```

#### useTelephonyLaunch - получение всех данных об операторе и серверах телефонии
```
    // Получаем состояние загрузки хэша
    const {loading, data, error} = useTelephonyLaunch();
    
    // Если не удалось получить можно вывести заглушку
    if (error) {
        return 'Нет данных для подключения к серверам телефонии'
    }
```

#### useTelephonyStatus - получение и управление статусом.

Статус это состояние агента на серверах телефонии в текущий момент.

```
    enum Status {
        CONNECTED = 'connected', // Подключен (может принимать звонки)
        DISCONNECTED = 'disconnected', // Отключен (не может принимать звонки)
        PAUSED = 'paused', // Отключен (не может принимать звонки) Отличие от статуса DISCONNECTED в том, что используется для учета статистики.
    }
```

```
    // Получаем состояние статуса
    const [{loading, data, error}, setStatus] = useTelephonyStatus();
    
    // Кнопка выхода с линии для оператора.
    return <button onClick={() => setStatus({status: Status.DISCONNECTED})}></button>
```

setStatus принимает и второй аргумент sub_status. Нужен для разделения например причин пауз.

```
    // Получаем состояние статуса
    const [{loading, data, error}, setStatus] = useTelephonyStatus();
    
    // Выставляет оператора на паузу с причиной smoking.
    return <button onClick={() => setStatus({status: Status.PAUSED, sub_status: 'smoking'})}></button>
```

Перейдем к описанию интерфейсов и методов телефонии

### Основные интерфейсы

#### UserAgent

https://jssip.net/documentation/3.5.x/api/ua/ - подробнее можно почитать тут

UserAgent может находиться в разных статусах:

```
    enum UserAgentStatus {
        CONNECTING = 'connecting', // Подключается к вебсокету
        CONNECTED = 'connected', // Подключен к вебсокету
        DISCONNECTED = 'disconnected', // Соединение потеряно
        ERROR = 'error', // Ошибка подключения
        REGISTERED = 'registered', // Успешно зарегистрирован на серверах.
    }
```

Библиотека отслеживает состояние статусов юзер агента. Если оператор в течение 15 секунд не сможет зарегистрироваться на серверах. То автоматика выведет его с линии


#### Session
Текущая сессия. По сути - звонок.

https://jssip.net/documentation/3.5.x/api/session/ - тут подробнее

```
    enum SessionStatus {
        WAITING = 'waiting', // Ожидание звонка
        ACTIVE = 'active', // В разговоре
        STARTING = 'starting', // Вызов пришел, но пока что не принят
        HOLD = 'hold', // Холд
    }

    enum SessionDirection {
        INCOMING = 'incoming', // Входящий вызов
        OUTGOING = 'outgoing', // Исходящий вызов
    }
```

#### Механизм смены регистраров

В библиотеку добавлен механизм смены регистраров. Раз в 15 секунд поллится ручка, которая отдает актуальный список, к каким серверам должен быть законнекчен клиент.
Если ответ ручки не совпадает с текущим списком регистраров, то есть 2 случая

случай 1: Нет активного звонка.

Мы отцепляемся от текущих регистраров и перецепляемся к новым

случай 2: Есть активный звонок.

Тут все немного сложнее, так как мы не можем сразу перейти на другие сервера, так как потеряем голосовой трафик с клиентом. Поэтому тут отложено при завершении вызова делаем то же самое что и в случае 1.
