#b-callouts-manager#

##Описание##
Блок предназначен для действий над уточнениями в группах.

###Автор###
[eemelin ](https://staff.yandex-team.ru/eemelin )

###Где используется###
b-callouts-selector - для удаления уточнения из баннеров в кампании

###Взаимодействие с другими блоками###
Опишите взаимодействие с другими блоками

###Модели###
Работает со списком моделей групп с идентификаторами params.groupsIds и именем params.groupModelName

##Как пользоваться и расширять##

На контекстном блоке b-callouts-manager

`
     BEM.create('b-callouts-manager', {
         groupModelName: 'm-group',
         groupsIds: this.params.groupsIds
     });

`

используем channel для выполнения действия

`
    this.channel('callouts').trigger('destroy', { id: id });
`

##Пример##

см. Как пользоваться и расширять
