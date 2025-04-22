# mfkit idm

[How to create IDM system](https://wiki.yandex-team.ru/users/pixel/kak-sozdat-svoju-sistemu-v-idm/)

[IDM role node tree](https://docs.yandex-team.ru/idm/guide/entities/role-tree)

## init

Initializes required idm configs:
`project.yml` - environment config (path, etc)
`testing.yml` - example roles config for testing environment
`production.yml` - example roles config for production environment

Usage:
```
mfkit init idm [-f]
```

## init-roles

Creates example YAML config

Usage:
```
mfkit idm init-roles <env> [-f]
```

Output YAML file:
```yaml
code: 0
roles:
  slug: role
  name: Role
  values:
    user:
      slug: user
      name: User
      roles:
        slug: as
        children:
          - slug: editor
            name: Editor
            roles:
              slug: section
              children:
                - slug: a
                  name: Section A
                - slug: b
                  name: Section B
    service:
      slug: service
      name: Service
      roles:
        slug: api
        children:
          - slug: ping
            name: Ping
```

## sync-roles

Converts YAML config to TypeScript at specified environment path in `project.yml`, validating YAML config format in between

Usage:
```
mfkit idm sync-roles
```

Output TS file:
```ts
/*
 * WARNING: This file generated automatically, please do not make any changes
 */

const enum ROLES {
    /** Role / User / Editor / Section A */
    ROLE_USER_AS_EDITOR_SECTION_A = '/role/user/as/editor/section/a/',

    /** Role / User / Editor / Section B */
    ROLE_USER_AS_EDITOR_SECTION_B = '/role/user/as/editor/section/b/',
    
    /** Role / Service / Ping */
    ROLE_SERVICE_API_PING = '/role/service/api/ping/'
}

export {ROLES};
```

## validate-roles

Validate YAML config and existing TS config at specified environment path in `project.yml`

Usage:
```
mfkit idm validate-roles
```

