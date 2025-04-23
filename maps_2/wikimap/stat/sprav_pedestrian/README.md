lib - основная функциональность, в eval_report есть if __name__ == "__main__": который сделан для запуска этого файла в нирване
ut - тесты, импортирующие основную функциональность
bin - тула для локального запуска
Расчётный день начинается с 03:00.
запуск
./bin/local_run \
    --task-type 'address' \
    --tasks '//home/maps/core/nmaps/production/pedestrian/address_tasks' \
    --export '//home/sprav/assay/tasker/walkers/maps/address_export' \
    --report 'Maps.Wiki/Sprav/Pedestrian.Address' \
    --statface-token **** \
    --yt-token **** \
Публикует  отчет на stat-beta  https://stat-beta.yandex-team.ru/Maps.Wiki/Sprav/Pedestrian.Address)
