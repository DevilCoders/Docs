# pause - приостановить выполнение сценария

```
# встать на паузу, пока кто-то смелый не прожмёт кнопку "resume" в интерфейсе
- name: pause indefinitely until king Arthur pulls the sword from the stone
  pause: null
```

Джоба встанет в состояние `paused`, из которого её можно будет вызволить при помощи прожатия кнопицы "Resume" в web UI на странице списка джобов:

![https://jing.yandex-team.ru/files/m-arefiev/Screenshot%202022-07-04%20at%2022.30.57.png](https://jing.yandex-team.ru/files/m-arefiev/Screenshot%202022-07-04%20at%2022.30.57.png)

Работает примерно как [https://docs.yandex-team.ru/ci/flow#manual-confirmation](Гендальф в Arcadia CI):

![https://docs.yandex-team.ru/docs-assets/ci/f844e9e1ef0dd85a53488f07ba27e2bd5f6669a6/ru/img/flow-manual-job.png](https://docs.yandex-team.ru/docs-assets/ci/f844e9e1ef0dd85a53488f07ba27e2bd5f6669a6/ru/img/flow-manual-job.png)

Область применения такая же – если в сценарии есть действия, решение о запуске которых принимается каждый раз индивидуально и вручную.
