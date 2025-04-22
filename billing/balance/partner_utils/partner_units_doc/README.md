Используется Sphinx и Mako.

Шаблон (mako) документации находится в `src_doc/index.rst.mako`.

В документацию попадают классы, у которых проставлен тэг `partner_units_doc` в docstring класса: `#tag1,#tag2,#partner_units_doc`.
Тэги удаляются из документации.
Настройки тэгов и исходных файлов с докстрингами в `main.py`.
Для получения юнитов, исходные классы импортируются.

Результат будет в `doc_output`: `index.html` (смотри также директорию `_static`) и `index.md`.

Примеры запуска в скриптах `gen.sh`, `gen.ps1`.

Модули нужные для запуска в `requirements.txt`.
Генерация markdown включена, но она какая-то хреновая: используется https://github.com/clayrisser/sphinx-markdown-builder.
Настройки генерации в `src_doc.conf.py`.

Как писать в ReST: https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html

Как писать docstring в sphinx: https://sphinx-rtd-tutorial.readthedocs.io/en/latest/docstrings.html

Ссылки на документацию:
 * https://www.sphinx-doc.org/en/master/usage/configuration.html
 * https://www.sphinx-doc.org/en/master/usage/theming.html#builtin-themes
 * https://www.sphinx-doc.org/en/master/man/sphinx-build.html
 * https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html#directive-automodule
 * https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html
 * https://sphinx-rtd-tutorial.readthedocs.io/en/latest/docstrings.html
 * https://github.com/clayrisser/sphinx-markdown-builder
