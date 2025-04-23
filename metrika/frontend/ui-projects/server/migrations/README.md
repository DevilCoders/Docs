# Migrations

В качестве инструмента миграций используется [TypeORM](https://github.com/typeorm/typeorm/blob/master/docs/migrations.md)

Миграции создаются под каждый сервис, который использует собственную независимую схему базы данных.

---
### Просмотр всех миграций

```
npm run migration:show:[SERVICE_NAME]:[ENV]
```

Если миграцию еще не раскатили, то она будет отмечена как `[ ]`, например:
```
 [X] Migration1642553020010
 [ ] Migration1642553020011
```

### Создание миграции
Название миграции должно соответствовать номеру тикета
```
npm run migration:create:[SERVICE_NAME] -- -n METR-47952
```

После выполнения этого скрипта будет сгенерирован файл миграции в формате `[timestamp]-[migrationName].ts` с двумя методами `up` и `down`.
- `up` должен содержать код, необходимый для выполнения миграции
- `down` выполняется при откате миграции

Пример миграции:
```(js)
export class AddColumn1642434303194 implements MigrationInterface {

    public async up(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.query(`ALTER TABLE "user" ADD "anyField" character varying NOT NULL`);
    }

    public async down(queryRunner: QueryRunner): Promise<void> {
        await queryRunner.query(`ALTER TABLE "user" DROP COLUMN "anyField"`);
    }
}
```
### Запуск миграции
```
npm run migration:run:[SERVICE_NAME]:[ENV]
```
Выполнит все ожидающие миграции и выполнит их в последовательности, упорядоченной по их меткам времени. Это означает, что все sql-запросы, написанные в `up` методах созданных вами миграций, будут выполнены

### Откат миграции
```
npm run migration:revert:[SERVICE_NAME]:[ENV]
```
Эта команда вызовит `down` в последней выполненной миграции. Если вам нужно отменить несколько миграций, вы должны вызвать эту команду несколько раз.
