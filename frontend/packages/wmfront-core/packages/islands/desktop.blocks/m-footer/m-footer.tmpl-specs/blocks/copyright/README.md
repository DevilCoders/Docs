# Зачем здесь эти шаблоны?

Во время сборки `tmpl-specs` используется упрощенное ядро `BEM.I18N`. Это ядро некорректно обрабатывает сложные ключи,
которые используются в шаблоне блока `copyrigth` в моде `wrapLink`.

Чтобы обойти эту нестыковку, специально для сборки `tmpl-specs` написан упрощенный шаблон моды `wrapLink` для блока
`copyright`. Оба шаблона (как `copyright.bemhtml.js`, так и `copyright.bh.js`), и даже файл с депсами
(`copyright.deps.js`) самым честным образом скопированы из репозитория
[islands@4.4.0](https://github.yandex-team.ru/lego/islands/tree/v4.4.0/common.blocks/footer/footer.tmpl-specs/blocks/copyright).

Без этих шаблонов блок `copyright` рендерит сплошную чушь:
```
<div class="copyright">© 2003–2016 link: {"content":"<a class="\&quot;copyright__link" footer__link\"="" href="\&quot;http://www.yandex.ru\&quot;">yandex</a>"}</div>
```
