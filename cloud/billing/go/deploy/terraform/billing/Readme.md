# Billing deploy via terraform

### Общая информация

В этой папке лежат инсталляции биллинга. В каждой папке лежат элементы инсталляций,
которые деплоятся через терраформ. Сейчас это только проверки juggler, возможно когда-нибудь
появится что-нибудь еще. Про общие правила использования и ркомендации можно прочитать в
`Readme.md` в папке выше.

### Как посмотреть/задеплоить какие-то изменения

Заходите в нужную папку и пишете `terragrunt plan`. Так вы увидите то, что поменяется. Чтоб
применить изменения пишете `terragrunt apply` и соглашаетесь с изменениями. Например:
```shell
cd preprod
terragrunt plan
... # вывел ваши изменения
terragrunt apply
... # вывел то, что применит
yes
```
