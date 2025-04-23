# Audio Recorder

Проект является форком [Github: AudioRecorder](https://github.com/Dimowner/AudioRecorder)

## Сборка

### Собрать с помощью Android Studio

* открыть проектв Android Studio
* выбрать нужный `buildVariant`
* собрать проект

### СБорка с помощью `gradlew`

* Посмотреть список возможных тасок gradle

```bash
./gradlew tasks
```

* Собрать Release можно так

```bash
./gradlew compileReleaseConfigReleaseSources  # выбираем нужную конфигурацию
./gradlew build                               # запускаем сборку
```

* Результат сборки можно найти

```bash
./app/build/outputs/apk/releaseConfig/release/app-releaseConfig-release.apk
```

### Запись звука через интенты

* установить приложение с выдачей пермишенов

```bash
adb install -r -g -t app/build/outputs/apk/debugConfig/debug/app-debugConfig-debug.apk
```

* запустить приложение

```bash
adb shell am start -n 'com.dimowner.audiorecorder.debug/com.dimowner.audiorecorder.app.main.MainActivity'
```

* пройти сплеш активити и настройки, можно командами:

```bash
adb shell input keyevent 23 && adb shell input keyevent 23
```

* запустить запись звука

| параметр интента | дефолтное значение | возможные значения |
| ------ | ------ | ------ |
| audio_format | wav | wav, m4a, 3gp |
| sample_rate | 16000 | 8000, 16000, 22050, 32000, 48000 |
| bitrate | 128000 | 48000, 96000, 128000, 192000, 256000 |
| channel_count | 1 | 1, 2, 4, 8, 16 |
| filename | null | любое имя файла, без формата |

```bash
adb shell am start-service -a com.dimowner.audiorecorder.ACTION_START_RECORD \
-e audio_format wav \
--ei sample_rate 16000 \
--ei bitrate 1 \
--ei channel_count 1 \
-e filename alice_001.wav
```

* остановить запись звука

```bash
adb shell am start-service -a com.dimowner.audiorecorder.ACTION_STOP_RECORD
```

* скачать файлы с девайса

```bash
adb pull /storage/emulated/0/Android/data/com.dimowner.audiorecorder.debug/files/Music/records
```

## ChangeLog

* поправлен gradlew
* поправлена поддержка горизонтальной ориентации для ТВ
* добавлен сервис для внешней записи звука через интенты
* поправлен краш во время открытия настроек на русской локали (не хватало айтемов)
* удалилены лишние переводы

* Число каналов для записи расширено до 16. Итого возможные варианты `{1, 2, 4, 8, 16}`.
  Протестировано для wav формата.
