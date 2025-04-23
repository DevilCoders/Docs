{% extends "telegram/base.md" %}
{% block body %}
{% if packages.size() > 1 %}
📦 Следующие пакеты собраны:
{% for pkg in packages %}
{%- if pkg.packageType == 'DEB' -%}
• [{{pkg.debPackageName}}]("https://c.yandex-team.ru/packages/{{pkg.debPackageName}}") версии {{pkg.version}}
{% endif %}
{%- if pkg.sandboxTicket != null -%}
• [{{pkg.moduleName}}]("https://sandbox.yandex-team.ru/resources?type={{pkg.sandboxResourceType}}") версии {{pkg.version}}
{% endif %}
{%- if pkg.packageType == 'RPM' %}{% for rpm in pkg.rpmPackages -%}
• [{{rpm.name}}]("https://c.yandex-team.ru/packages/{{rpm.name}}") версии {{rpm.version}}
{% endfor %}{% endif -%}
{% endfor -%}
{% else %}
📦 Собран пакет {% if packages.get(0).debPackageName %}[{{packages.get(0).debPackageName}}]("https://c.yandex-team.ru/packages/{{packages.get(0).debPackageName}}"){% else %}[{{packages.get(0).moduleName}}]("https://sandbox.yandex-team.ru/resources?type={{packages.get(0).sandboxResourceType}}"){% endif %} версии {{packages.get(0).version}}{% endif %}{% endblock body %}