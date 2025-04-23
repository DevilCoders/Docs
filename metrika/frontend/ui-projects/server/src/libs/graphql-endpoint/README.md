# GraphQL endpoint

Фасад над официальной реализацией graphQL сервера, позволяющий описать endpoint в декларативном виде.

## Endpoint Api

Представлено единственным методом execute, выполняющим query / mutation и, возваращющим результат

```
interface GraphQLEndpointApi<TContext extends DefaultGraphQLContext> {
    execute(query: string, context: TContext, variables?: object): Promise<ExecutionResult>;
}
```

Получить инстанс graphql endpoint api можно, вызвав функцию createGraphQLEndpoint, в которую надо передать классы, 
определяющие композитные типы, перечислимые типы и контроллеры, размеченные декораторами (см. раздел «Декораторы»)

```
function createGraphQLEndpoint<TContext extends DefaultGraphQLContext>({
    types: typeTargets,
    controllers,
}: GraphQLEndpointParams)
```

Пример:
```
createGraphQLEndpoint({
    types: [
        UserEntity,
        UserContactEntity,
        UsersFilterInput
    ],
    controllers: [
        UserController
    ]
})
    .execute(
        'query test1($test: [String]) { users(filter: { ids: $test }) { names, userId, isAvailable, contact { phone } } }',
        { getLogger: () => Logger.withContext('gql') },
        { test: ['1'] }
    )
    .then(res => console.log(JSON.stringify(res)));
```


## Декораторы

### Как указывать типы в декораторах?

Если в качестве агрумента или возвращаемого типа в дектораторе требуется указать скалярный тип, достаточно использовать соответствующий скалярный тип из библиотек `graphql`. При использовании композитного типа требуется обернуть его с помощью метода `GraphQLTypeWrap.of`.
При использовании перечислимого типа – с помощью метода `GraphQLEnumWrap.of`.

Для указания того, что значение типа является Non-Null, достаточно обернуть тип с помощью метода `GraphQLNonNullWrap.of`.


Для указания массива необходимо передать тип элемента массива в метод `GraphQLList.of`.

Пример:

```
@Entity('UserContact')
class UserContactEntity {
    @EntityField({ type: GraphQLString })
    phone?: string;

    @EntityField({ type: GraphQLString })
    email?: string;
}

@Entity('User')
class UserEntity {
    @EntityField({ type: GraphQLEnumWrap.of(UserRole) })
    role!: UserRole;

    @EntityField({ type: GraphQLNonNullWrap.of(GraphQLID) })
    id!: string;

    @EntityField({ 
        type: GraphQLList.of(GraphQLNonNullWrap.of(
            GraphQLTypeWrap.of(UserContactEntity)
        ))
    })
    contacts?: UserContactEntity[];
}
```

Эквивалентная graphQL схема:

```
type UserContactEntity {
    phone: String
    email: String
}

type UserEntity {
    id: ID!
    contacts: [UserContactEntity!]
}
```


### GraphQLEnum
Декоратор, определяющий перечислимый тип. Все перечислимые типы следует хранить на полях выделенного статического класса.
Этот класс следует передать в функцию `createGraphQLEndpoint` при создании graphql endpoint.

Пример:
```
enum UserRole {
    Admin = 'ADMIN',
    Operator = 'OPERATOR',
    Guest = 'GUEST'
}

class EnumTypes {
    @GraphQLEnum({ name: "UserRole" })
    public static readonly userRole = UserRole;
}

//…

createGraphQLEndpoint({
    types: [/* … */],
    enumTypes: EnumTypes,
    controllers: [/* … */]
})
```

### GraphQLInput
Декоратор, определяющий Input тип, который используется в аргументах graphql запросов.

Пример:
```
@GraphQLInput('UsersFilterInput')
class UsersFilterInput {
    @EntityField({ type: GraphQLList.of(GraphQLString) })
    ids!: Array<string>;
}

@GraphQLInput('CreateUserInput')
class CreateUserInput {
    @EntityField({ type: GraphQLString })
    firstName!: string;

    @EntityField({ type: GraphQLString })
    lastName!: string;
}
```

### GraphQLOperationArgs / GraphQLArg
Декораторы, определяющие наборы аргументов graphql

Пример:
```
@GraphQLOperationArgs()
class UsersQueryArgs {
    @GraphQLArg({ type: GraphQLTypeWrap.of(UsersFilterInput) })
    filter!: UsersFilterInput;
}

@GraphQLOperationArgs()
class CreateUserMutationArgs {
    @GraphQLArg({ type: GraphQLTypeWrap.of(CreateUserInput) })
    data!: CreateUserInput;
}
```         

### GraphQLController / GraphQLQuery / GraphQLMutation
Декораторы, определяющие класс и его методы-обработчики graphql queue / mutation  

Пример:
```
@GraphQLController()
class UserController {
    @GraphQLQuery({ 
        name: 'users', 
        type: GraphQLList.of(GraphQLTypeWrap.of(UserEntity)), 
        argsType: UsersQueryArgs 
    })
    getUsers(
        args: UsersQueryArgs, 
        context: DefaultGraphQLContext
    ): UserEntity[] {
        context.getLogger().info(`args: ${JSON.stringify(args)}`);
        const user = new UserEntity();

        user.isRemoved = false;
        user.userId = 'test';
        user.names = [];

        return [user];
    }

    @GraphQLMutation({
        name: 'createUser', 
        type: GraphQLTypeWrap.of(UserEntity), 
        argsType: CreateUserMutationArgs 
    })
    public createUser(
        args: CreateUserMutationArgs, 
        context: DefaultGraphQLContext
    ): UserEntity {
        const result = new UserEntity();
        //…
        return result;
    }
}
```

### Entity / EntityField
Декораторы, определяющие graphql тип и резолвинг его полей  

Пример:
```
@Entity('UserContact')
class UserContactEntity {
    @EntityField({ type: GraphQLString })
    phone!: string;
}

@Entity('User')
class UserEntity {
    @EntityField({ type: GraphQLString })
    userId!: string;
    login!: string;
    firstName!: string;
    lastName!: string;
    isRemoved!: boolean;

    @EntityField({ type: GraphQLList.of(GraphQLString) })
    names!: string[];

    @EntityField({ type: GraphQLBoolean })
    isAvailable(): boolean {
        return !this.isRemoved;
    }

    @EntityField({ 
        name: 'contact', 
        type: GraphQLList.of(GraphQLList.of(GraphQLTypeWrap.of(UserContactEntity))) 
    })
    getContact(): UserContactEntity[][] {
        return [[{
            phone: 'test-phone'
        }], [{
            phone: 'test-phone1'
        }, {
            phone: 'test-phone2'
        }]];
    }
}
```

