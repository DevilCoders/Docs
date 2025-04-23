{% if packages.size() > 1 %}
📦 Следующие пакеты собраны:
{% for pkg in packages %}
{%- if pkg.packageType == 'CONDUCTOR' -%}
• {{pkg.debPackageName}} версии {{pkg.version}}: https://c.yandex-team.ru/packages/{{pkg.debPackageName}}
{% endif %}
{%- if pkg.packageType == 'SANDBOX' -%}
• {{pkg.moduleName}} версии {{pkg.version}}: "https://sandbox.yandex-team.ru/resources?type={{pkg.sandboxResourceType}}"
{% endif %}
{%- if pkg.packageType == 'RPM' %}{% for rpm in pkg.rpmPackages -%}
• {{rpm.name}} версии {{rpm.version}}: "https://c.yandex-team.ru/packages/{{rpm.name}}"
{% endfor %}{% endif -%}
{% endfor -%}
{% else %}
📦 Собран пакет {% if packages.get(0).debPackageName %}{{packages.get(0).debPackageName}}: "https://c.yandex-team.ru/packages/{{packages.get(0).debPackageName}}"{% else %}{{packages.get(0).moduleName}}: "https://sandbox.yandex-team.ru/resources?type={{packages.get(0).sandboxResourceType}}"{% endif %} версии {{packages.get(0).version}}{% endif %}{% endblock body %}