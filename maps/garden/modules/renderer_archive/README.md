# renderer_archive

[Архивы тайлов подложки](https://st.yandex-team.ru/MAPSRENDER-3165).
Модуль на основе дампа renderer_denormalization_dump создает тайловый датасет в tilemill и добавляет его как пользовательский датасет в Картограф, на основе дизайна renderer_map_stable_bundle создает ветку в Картографе и подменяет в нем датасет подложки на сгенерированный.

Удаление релиза:
```
ya make -r maps/garden/modules/renderer_archive/tools/remove_archive

export AWS_ACCESS_KEY_ID=`cat ~/.aws/aws_id`
export AWS_SECRET_ACCESS_KEY=`cat ~/.aws/aws_key`

./maps/garden/modules/renderer_archive/tools/remove_archive/remove_archive --contour datatesting --release-name 22.04.01-0
```
