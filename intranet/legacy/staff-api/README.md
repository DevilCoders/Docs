#### Выкатить на тестинг
`releaser release`

#### Докатить в продакшн
`releaser deploy -e tools_staff-api_production`

#### Генерация ресурсов по json схемам
`~/arcadia/junk/cracker/generate/schema-generate -o ./internal/api/resources.go -p api ./internal/api/schemas/room.json ./internal/api/schemas/equipment.json ./internal/api/schemas/position.json ./internal/api/schemas/office.json ./internal/api/schemas/departmentstaff.json ./internal/api/schemas/group.json ./internal/api/schemas/person.json  ./internal/api/schemas/table.json ./internal/api/schemas/organization.json ./internal/api/schemas/groupmembership.json ./internal/api/schemas/common.json`

`ya tool go fmt ~/arcadia/intranet/staff-api/internal/api/resources.go`