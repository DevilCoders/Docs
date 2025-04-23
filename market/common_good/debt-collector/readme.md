Настройка проекта:
1. Перейти в директорию проекта и запустить скрипт generate_project.sh (флаг -i указывает директорию для генерации проекта):
    ```bash
    cd ~/arcadia/market/common_good/debt-collector
    bash generate_project.sh -i ~/projects
    ```
2. Открыть сгенерированный проект помощью idea и выбрать jdk17 в File -> Project Structure... -> ProjectSettings -> Project -> SDK
<br>
Если jdk17 отсутствует, скачать его можно, выполнив команду:
    ```bash
    ya tool java17 --print-path
    ```
3. Запустить проект, используя run configuration "Run service (generated)" (конфигурация подтянется автоматически при генерации проекта)
