

### Завести презентацию для нового Демо спринта

```bash
arc checkout -b update_demo
cp arcadia/portal/demo/slides/template.html arcadia/portal/demo/slides/77.html
arc add arcadia/portal/demo/slides/77.html
# Меняем __ на номер спринта в `77.html` в первом слайде
arc commit -m 'update demo'
arc push --set-upstream users/bdevin/update_demo
arc pr create -m "Update morda demo"
```

Открыть пр по ссылке, проскипать проверки, вмёржить

### Как добавить слайды?
1. Переходим в Arcadia на актуальную презентацию, например
https://a.yandex-team.ru/arc_vcs/portal/demo/slides/120.html
2. Редактируем. [Примеры разметки слайдов](https://a.yandex-team.ru/arc_vcs/portal/demo/slides/sample.html)
![](https://jing.yandex-team.ru/files/4eb0da/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_947.png)

3. Создаём ревью
![](https://jing.yandex-team.ru/files/4eb0da/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_948.png)

4. Выключаем проверки, ждём мёржа
![](https://jing.yandex-team.ru/files/4eb0da/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_949.png)

5. Готово
![](https://jing.yandex-team.ru/files/4eb0da/%D0%92%D1%8B%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_950.png)

Чуть более развернутый вариант есть на [вики](https://wiki.yandex-team.ru/morda/qa/kak-sdelat-slajjd-dlja-demo/).

