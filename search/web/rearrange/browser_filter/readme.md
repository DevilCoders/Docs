# Фильтры по браузерам

Фильтрация производится блендерной командой по выставленному правилом серчпропу.

Чтобы добавить фильтрацию нужно добавить фильтр в [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/rearrange/browser_filter/config.json) или в [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/conf/conf.json) или в [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/rearrange.fast/browser_filter/config.json):  

```
<название нового фильтра> : {
  "Enabled": <включить/выключить работу нового фильтра. Влияет на выставление серчпропа.>,
  "BrowserRule" : <Конфигурация браузера>,
  "SetSearchProp": <текст серчпропа, который будет выставлен, если браузер удовлетворяет конфигурации BrowserRule>,
}
```

Если добавить одинаковые названия фильтра в разные конфиги, то они НЕ перезапишутся и SetSearchProp может быть выставлен дважды для одного назания