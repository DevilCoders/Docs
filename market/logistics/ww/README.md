## Сервис генерации и конвертации документов Доставки

### Локальный запуск

В Idea, в классе LogisticsWw с помощью интеграции со spring, нажимаем кнопку "play" рядом с именем класса, далее
`Edit "LogisticsWW"….`


**В следующих полях выставить значения:**


Environment variables:
PROPERTIES_DIR=src/main/properties.d/

Active profiles: 
local

Working directory:
$MODULE_WORKING_DIR$

### Документация API
Локально доступна http://localhost:8081/swagger-ui.html