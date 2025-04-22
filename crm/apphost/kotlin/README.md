# Kotlin CRM Apphost nodes

## Directory structure

- common - core functionality of Kotlin apphost nodes
- dal - Hibernate database mappings _TODO: delete_
- database - database migrations and root for generated jOOQ's code
- handlers - implementation of nodes _TODO: rename to `services`_
- services - executable microservices - applications that hosts a set of nodes _TODO: rename to `apps`_

{% include [Debugging](services/_debugging.md) %}

{% include [CodeRules](../../library/kotlin/docs/_coderules.md) %}
