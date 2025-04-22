Hypotheses
===

## Summary

Hypothesis is an educated guess about inaccuracy (or simply incompleteness) in our data made by some automatic algorithm. Project contains such hypotheses generating algorithms.

All hypotheses are sent to nmaps feedback and then processed by our team of cartographers. From the nmaps point of view it looks something like this

![NMaps interface](https://jing.yandex-team.ru/files/ngng/Screenshot%202020-09-28%20at%2012.06.34.png)

## Hypotheses

| Name | NMaps name | Description | Maintainers info |
| --- | --- | --- | --- |
| [Rips](rips) | geoq-rips | Tries to find missed roads or inaccuracies by analyzing unmatched user tracks. | Sandbox schedulers: [(100173)](https://sandbox.yandex-team.ru/scheduler/100173) |
| [Loose signals](loose_signals) | geoq-no-nearby-geometry | Tries to find missed roads by unmatched signals. | Sandbox schedulers: [(85989)](https://sandbox.yandex-team.ru/scheduler/85989) |
| [Manoeuvres](manoeuvres) | geoq-forbid-manoeuvre, geoq-allow-manoeuvew | Tries to find inaccuracies in the road graph by analyzing user turns from one edge of road graph to another (called manoeuvres).<br/>Outputs two types of hypotheses: manoeuvres to allow and manoeuvres to forbid. | Sandbox schedulers: [(106594)](https://sandbox.yandex-team.ru/scheduler/106594) |
| [OSM diff](osm) | geoq-roads-d1 | Tries to find missed roads by analyzing OSM-vs-Yandex.Maps diffs. | Sandbox schedulers: [(74577)](https://sandbox.yandex-team.ru/scheduler/74577) |
| [Flats](flats) (on halt) | geoq-flats | Tries to find flat ranges which have enough info to complete them. | Sandbox schedulers: [307016 stable](https://sandbox.yandex-team.ru/scheduler/307016) <br/> [275487 testing](https://sandbox.yandex-team.ru/scheduler/275487) |


## Maintainers

[Geo quality team](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/)

## Quality

Charts can be found [here](https://dash.yandex-team.ru/62q89j2upqaq3). Quality is represented by two tabs: "Гипотез загружено" *(number of uploaded hypotheses)* and "Гипотез с правками" *(percent of accepted hypotheses)*.

The source of these charts is the Statface Report, which can be found [here](https://stat.yandex-team.ru/Maps.Wiki/Others/NmapsFeedback). Look at "Создано" for the number of uploaded hypotheses and "Полезный фидбэк (% с правками)" for the percent of accepted hypotheses.
