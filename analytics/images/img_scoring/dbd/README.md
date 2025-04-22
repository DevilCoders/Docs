# Images Doc-by-Doc

### Локальный запуск

1. Скачать проект:
```
svn checkout svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/analytics/images/img_scoring/dbd
cd dbd
```
2. Скачать данные: разметка документов на аспекты и результаты толоки 12 раундов:
```
make download_sample
```
3. Запустить расчёт предсказаний dbd_score и кликовой добавки для нескольких дефолтных бустов
```
make score
```
4. Посмотреть отчёт
```
open index.html
```

### Возможности dbd:
* Вьюер предсказания % пар толокеров и кликовой добавки по любому бусту: `make score`
* Вьюер топ/хвост запросов с предсказаниями таргета по любому бусту `make top_queries`
* Вьюер сравнения DbD по раундам `make round`
* Вьюер предсказания dbd, только у картинок по хоткею [s] показывается saliency_map `make saliency`
* Посчитать долю урлов, которые меняют порядок от раунда к раунду (т.е. сходимость) `make rounds_similarity`
* Посчитать предсказания исходных предпочтений толокеров по `dbd_score` и `Pscore` (т.е. шумность модели) `make noise`

### Ссылки:
* Задача — https://st.yandex-team.ru/MMA-1009
* Презентация DbD на семинаре https://yadi.sk/i/bO2TapUu3TSUYb
* Проект в толоке — https://toloka.yandex.com/requester/project/11034
* https://nda.ya.ru/3UCeDR — граф в нирване с отчётами на полном пуле
* https://nda.ya.ru/3UCeDT — граф в нирване с отчётами на семпле запросов, как локальный запуск
* https://nda.ya.ru/3UCeFH — граф в нирване с разметкой в толоке 12-го раунда
