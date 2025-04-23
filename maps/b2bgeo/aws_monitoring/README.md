# Конфиги для kube-prometheus

## Получение
Наши правки конфигов хранятся в виде патча к оригинальному репозиторию. Для получения последней версии, патч нужно применить:

```bash
git clone https://github.com/prometheus-operator/kube-prometheus && cd kube-prometheus
git checkout 2ba16bb38543c7cb73119254b2895d073e410577
GIT_COMMITTER_EMAIL='a@a.a' git am ../kube-prometheus.gitpatch
```

Дальше можно производить выкатку, согласно README репозитория [kube-prometheus](https://github.com/prometheus-operator/kube-prometheus).

## Обновление

Для внесения изменений в патч, нужно закоммитить изменения в репозиторий и получить обновлённый патч:

```bash
git format-patch --stdout 2ba16bb38543c7cb73119254b2895d073e410577 > ../kube-prometheus.gitpatch
```
