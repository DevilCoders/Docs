Overview
===
Эта библиотека предоставляет доступ к мгновенным значениям потребления процессора текущим процессом.

NCpuLoad::TInfo
===
Структура, содержащая информацию о загрузке процессора:
* `User` - пользовательская загрузка;
* `System` - системаня загрузка;

NCpuLoad::Get()
===
Возвращает NCpuLoad::TInfo с текущими значениями.
