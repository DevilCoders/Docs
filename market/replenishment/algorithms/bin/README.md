# Бинарники Алгоритмов Репленишмента

## Основные
"Калькуляторы" (основные исполнители полезной нагрузки в контексте Nirvana)
- [vicugna (ex alpaca)](./vicugna)
- [common_calculator (legacy python2)](./common_calculator)
- [common_calculator_v2 (new python3)](./common_calculator_v2/README.md)

## graph_generator

Приложение граф-генератор для replenishment.
- [graph_generator](./graph_generator)

Сам класс ReplenishmentGraph лежит в модуле `market/replenishment/algorithms/lib/graph/graph.py`
- [ReplenishmentGraph](../lib/graph.py)

## run.sh

Скрипт для локальных запусков и удобства отладки

    По умолчанию аркадия ищется в $HOME/arc/arcadia
    Если у вас каталог аркадии примонтирован в отличное от $HOME/arc/arcadia место,
    то нужно создать переменную окружения ARC_HOME с указанием текущего местополжения аркадии

```shell script
echo '===='
echo 'LOCAL RUN replenishment graph_generator'
echo '===='
if [ -z "${ARC_HOME}" ]; then
  arcadia_home=$HOME/arc/arcadia
else
  arcadia_home="${ARC_HOME}"
fi
echo "* arcadia_home = $arcadia_home"
if [ ! -d $arcadia_home ]
then
    echo "arcadia должна быть примонтирована в `echo $arcadia_home`"
    echo "создайте ссылку существующего арка на ~/arc или примонтируйте арк заново"
    exit 0001
fi
repl_home=$arcadia_home/market/replenishment/algorithms
echo "* build $repl_home/bin"
echo "* /common_calculator"
ya make -r --yt-store $repl_home/bin/common_calculator
echo "* /common_calculator_v2"
ya make -r --yt-store $repl_home/bin/common_calculator_v2
echo "* /vicugna"
ya make -r --yt-store $repl_home/bin/vicugna
echo "* build $repl_home/bin/graph_generator"
ya make -r --yt-store $repl_home/bin/graph_generator
echo '* run graph_generator'
$repl_home/bin/graph_generator/graph_generator \
--calc_app=$repl_home/bin/common_calculator/common_calculator \
--calc_v2_app=$repl_home/bin/common_calculator_v2/common_calculator_v2 \
--alpaca_app=$repl_home/bin/vicugna/alpaca \
--secret_name=replenishment_nirvana_yt_token \
"$@"
```
