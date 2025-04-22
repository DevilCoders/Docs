{% cut "Пример вывода команды для разных состояний предыдущего релиза" %}

{% list tabs %}

- выложен

    ```text
    DIRECT-124258 1.7132653-1 closed / App: java_jobs / Регулярный релиз 19
    ### current cmd: inspect-issue

    app: java-jobs, stage: testing, FINISHED
    DIRECT-124258 1.7132653-1 closed / App: java_jobs / Регулярный релиз 19

    inspect-issue: done
    ```

- дотестирован, но ещё не выложен

    ```text
    DIRECT-124422 1.7140345.7147312-1 readyToDeploy / App: java_web / Доделки по промокодам
    ### current cmd: inspect-issue

    app: java-web, stage: testing, FINISHED
    DIRECT-124422 1.7140345.7147312-1 readyToDeploy / App: java_web / Доделки по промокодам

    inspect-issue: done
    ```

- ещё тестируется

    ```text
    DIRECT-124260 1.7132863-1 testing / App: java_intapi / Сборка от 2020-07-20
    ### current cmd: inspect-issue

    app: java-intapi, stage: testing, FINISHED
    DIRECT-124260 1.7132863-1 testing / App: java_intapi / Сборка от 2020-07-20

    inspect-issue: done
    ```

{% endlist %}

{% endcut %}

Если в её выводе указано **FINISHED** — всё хорошо, можно собирать новый релиз.  
Если вывело только **stage: testing** (без FINISHED), значит предыдущий релиз ещё тестируется — новый собирать рано.  
Ещё может упасть с ошибкой "**can't get lock for stage testing, stop**" — прямо сейчас кто-то другой собирает этот релиз.
