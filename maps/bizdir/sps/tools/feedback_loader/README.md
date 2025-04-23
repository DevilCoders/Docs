Инструмент для генерации реальных сигналов по [пользовательскому фидбеку](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/fbapi/feedback_task)
для тестирования Системы приема правок.

Параметры запуска:
- `--filter-by-rubrics` - сгенерировать сигналы только для организаций из ограниченного списка рубрик
- `--add-features` - добавить в сигнал признаки из фидбека, по дефолту не добавляются

Пример запуска:
```
./feedback_loader --verbose --count 10 --acceptor "https://sps-workstation-testing.n.yandex-team.ru/v1/signal/add" --geodata geodata6.bin
```
