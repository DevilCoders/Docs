# Maps Front Guidelines

## What is guidelines?
There are several prerequisites which should be taking into account:
* Yandex infrastructure is very changeable and our services must make these new requirements
* We have some best practices and we want to apply them to all our servies
* Sometimes a bug is found in one of our servies and we realise that other servies can be harmful as well
* We want to make our services more consistent for easy maintaining

So to meet these requirements a special mechanism is created. We called them guidelines. Guidelines are run periodically to keep your service up to date.

Guidilines contain a set of rules. Each rule is an integration test which can get data from any internal service (Deploy, Juggler, Awacs, and etc) and check these data to satisfy our requirements.

If a service doesn't meet any of our requirement, a bugtracker ticket will be created with detailed information how to fix these inconsistency.

Our guidelines is like integration tests for our services. We even use the test framework to run them.

{% if version > '0' %}
Собрана версия: {{version}}
{% endif %}
