# Что такое и зачем нужны SPI?

**SPI (Site Production Incidents)** - это [очередь тикетов](https://st.yandex-team.ru/SPI/order:updated:true/filter?resolution=empty()), используемая для того, чтобы зафиксировать инцидент. Тикет создается при любом воспроизводящемся нарушении работы того или иного сервиса Яндекса.

В **SPI**, обычно, складывается вся информация связанная с инцидентом и ведется его разбор. В число информации входят:
 
 - Название инцидента
 - Компонента
 - Испольнитель
 - Временные рамки
 - Описание
 - Что во время инцидента видели пользователи
 - Действия дежурного
 - Анализ
 - Диагностика
 - Меры предотвращения
 - К каким проблемам относится
 - Смежные сервисы, которые затронуло инцидентом

Ежедневно создается более 30 **SPI** тикетов. Поэтому были придуманы удобные инструменты для оперативного создания тикетов, они будут рассмотрены далее.
