# yandex-du-dscribe-upload-conf

### Зачем это нужно
Для возможности запуска dscribe-upload-files.pl с одинаковыми параметрами (командной строки) в продакшене и на тестовых средах.

### Что делает при установке пакета
Создает симлинк `/etc/dscribe/dscribe-upload.yaml` зависимости от типа окружения (предоставленного пакетом yandex-environment) на:
- `/etc/dscribe/dscribe-upload-files.yaml` - в продакшене
- `/etc/dscribe/dscribe-upload-files-np.yaml` - во всех остальных окружениях
Симлинк создается только если соответствующий файл существует.

### Что делает при удалениии пакета
Удаляет `/etc/dscribe/dscribe-upload.yaml` только если он существует и является симлинком

### Сборка
c ppcdev: `ya package --debian --publish-to direct-trusty direct/packages/yandex-du-dscribe-upload-conf/pkg.json`

