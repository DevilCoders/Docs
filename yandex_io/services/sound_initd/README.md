# SoundInit

SoundInit используется при настройке устройства для передачи звуком (частотной модуляцией) одноразового токена
для авторизации и данных о wifi.

Код из этого репозитория используется только на устройствах для приема звука.

В android ПП используется
```
https://bitbucket.browser.yandex-team.ru/projects/ML/repos/quasar/browse/android/sounddatatransfer/src/main/java/ru/yandex/quasar/sounddatatransfer
```
В IOS ПП
```
https://bitbucket.browser.yandex-team.ru/projects/MA/repos/mobile-yandex-client-ios/browse/QuasarKit/QuasarKit/SonicTransfer
```

Настройки протокола заданы в виде констант в soundUtils.h. Просто так менять их нельзя, т.к. те же константы
дублируются в других репозитоиях. Ниже константы обозначаются так: [constant]

## Передаваемое сообщение

Для передачи используются [BITS] битовые чанки.

Формат сообщения:

< start handshake > < protocol version > < payload > < end handshake >

< start handshake > и < end handshake > - метки, по которым принимающая сторона определяет начало и конец
                                          сообщения. Их чанки (частоты) заданы в [HANDSHAKE_START] [HANDSHAKE_END].
< protocol version > - 2 чанка задают версию протокола и ее хеш сумму.
< payload > - любое количество чанков.

Каждому чанку в конечном пилюке соответствует своя частота длительностью [DURATION] секунды согласно формуле:

frequency = [START_HZ] + chunk * [STEP_HZ]

## Парсинг звука

Для распознания записываем звук фрагментами, в каждом из которых через преобразование Фурье получаем все
частоты и выбираем самую громкую (с максимальной амплитудой). Частота переводится обратно в [BITS] чанк
(берется ближайшая возможная частота).

Поскольку запись фрагментов не синхронизирована с проигрыванием чанков с телефона, в один фрагмент записи
может попасть две разные частоты из пилюка (кусочки двух разных чанков), в таком случае выбирание самой
громкой частоты не корректно.

Поэтому записываем фрагменты длиной [DURATION] / [SPLIT_CHUNKS]. Тогда у нас получится [SPLIT_CHUNKS]
подпоследовательностей
```
a[i + shift] I = 0..n, shift = 0..[SPLIT_CHUNKS]
```
хотя бы в одной из которых все фрагменты будут попадать ровно на одну частоту (один чанк). Нужную
подпоследовательность мы ищем перебором c проверкой хеш суммы.


## <payload>

### Массив байт

Передаваемое сообщение приводится к массиву байт

### Хеш сумма

От полученного массами байт берется crc32 хеш сумма, от которой берутся [CHECKSUM_BYTES] младших байт и
добавляются в конец этого же массива.

Проверка этой хеш суммы дает нам понять, взяли ли мы нужную из [SPLIT_CHUNKS] подпоследовательностей.

###  Преобразование к массиву [BITS] чанков

### Избыточное кодирование

Полученный массив бьется на группы по [MAX_BYTES_PER_CHUNK] (сори за CHUNK в названии, это другой чанк),
каждая такая группа кодируется кодом Рида - Соломона над полем [GALOIS_FIELD] и заменяется массивом из
[MAX_BYTES_PER_CHUNK] + [FEC_BYTES] чанков.

В итоге полученный массив чанков отправляется пилюком.

## Немного про Рид - Соломона

Реализация кода Рид - Соломона и полей Галуа, что в нем используются - порт из:

```
https://github.com/zxing/zxing/tree/master/core/src/main/java/com/google/zxing/common/reedsolomon
```

В нашем случае код строится над полем
```
[GALOIS_FIELD] = GF(16) с примитивом x^4 + x + 1
```
Поэтому
```
[MAX_BYTES_PER_CHUNK] = 16 - 1 = 15
```
```
[BITS] = log2(16) = 4
```
Код Рид - Соломона может исправить до [FEC_BYTES] / 2 ошибок в каждой группе по  [MAX_BYTES_PER_CHUNK] + [FEC_BYTES] из <payload>. Большее количество ошибок код Рид Соломона может и не заметить, поэтому нужна хеш сумма <payload> для проверки.

## Отправляемые данные

Мы отправляем

- тип wifi сети [OPEN, WPA, WEP, UNKNOWN]
- хеш ssid в cлучае UNKNOWN или длину ssid в байтах + сам ssid в ином
- длину пароля в байтах и сам пароль
- длину xToken и cам xToken

Хеш ssid - два младших байта java функции, которая берется от строки в utf16. См. soundUtils::javaStyleStringHash

Парсится payload в SoundInitEndpoint::parseInitData

## Немного про код

Входная точка - SoundInitEndpoint.
SoundInitEndpoint ждет сообщения startInit от FirstRunEndpoint, после чего подсоединяется к audiod, запускает
SoundDataReceiver и подает ему звук через AudioStream.

EncoderDecoder по-кусочно декодирует полученное сообщение, SoundDataReceiver дергает колбек onDataReceived,
SoundInitEndpoint парсит полученные байты, находи wifi по хешу и отправляет запрос в firstrund на
подключение по http (это та же ручка, которую дергает ПП при настройке через колоночную точку доступа)
