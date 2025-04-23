#icon

Блок с иконками - общие для Директа и Коммандера  
Конкретная иконка определяется модификаторами вида size-13_info, size-16_delete


##Mods
**размер:**
size-13 (size-16):
- info      #информация 
- notice    #предупреждение
- delete    #удалить   
......


**тема:**
theme:   
- light           #прозрачность (или лайтовость): opacity 0.3
- ...    


##Examples

иконка в первозданном виде  
```
{
    block: 'icon',
    mods: { 'size-16': 'plus' }
}
```

иконка с opacity: 0.3 по гайду
```
{
    block: 'icon',
    mods: { 'size-16': 'plus', 'theme': 'light' }
}
```




##Appearance

icon|name
---|---
![](./_size-16/icon_size-16_edit.svg)       |edit
![](./_size-12/icon_size-12_info.svg)       |info  
![](./_size-12/icon_size-12_notice.svg)     |notice  
![](./_size-16/icon_size-16_delete.svg)     |delete  
![](./_size-16/icon_size-16_plus.svg)       |plus    



##Мейнтейнеры
[@anyakey](https://staff.yandex-team.ru/anyakey)   
[@johnson](https://staff.yandex-team.ru/johnson)





#####Способы просмотреть, как выглядит иконка



>mac  
>открыть директорию с svg в finder  
>выделить файл svg  
>нажать "пробел" - откроется окно предпросмотра 



