# allure-sandbox-controls
Дополнительные страницы к Allure-отчету в sandbox

Содержит RunListener, который добавляет к каждому отчету по каждому тесту аттач с именем теста и ссылкой на текстовый лог.

RunListener подцепляется к паку либо через pom, либо через AspectJ (врезкой в ParentRunner JUnit'а)

Для AspectJ нужно добавить в пак тестов файл aop.xml в ресурсы
