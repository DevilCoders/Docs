# Ядро внутренних инструментов (internaltools-core)

### Что это?

internaltools-core - это базовые компоненты для построения внутренних инструментов Директа. 
В модуле описаны интерфейсы, которые нужно реализовывать для добавления своих инструментов, 
объявлены аннотации которые помогут в этом, а так же содержится код, который прячется за 
обработкой всего вышеперечисленного.

#### Для чего можно использовать внутренние инструменты?

Внутренние инструменты позволяют сгенерировать веб-страницу с формой, при отправке которой выполняется какое-то
действие на бекенде и отдается ответ в виде таблицы. Преимуществом использования является то, что для этого не нужно
писать никакого фронтового кода, пользовательский интерфейс генерируется автоматически. На текущий момент мы считаем,
что такие страницы могут использоватся только внутренними пользователями.

На базе internaltools можно реализовать:

- страницу, позволяющую поменять какие-то настройки Директа, хранящиеся в базе данных, например, процент запросов,
  отправляемых на препрод БК
- страницу, на которой менеджер может заказать построение какого-нибудь долгого офлайнового отчета или скачать ранее 
  построенный отчет, при условии что страница будет отдавать только список уже заказанных менеджером отчетов, а сами 
  отчеты будут строиться где-то в другом месте, например в java-jobs.

На базе internaltools сейчас нельзя делать пользовательские интерфейсы со сложной логикой работы, например с полями 
для ввода, который при модификации изменяют содержимое остальной страницы или состав других полей ввода

### Как этим пользоваться?

#### Как подключить внутренние инструменты?

Внутренние инструменты смотрят наружу через два класса:

 - `ru.yandex.direct.internaltools.core.InternalToolProxy` - обертка над инструментом, которую нужно 
   использовать для его вызова. Обертка содержит развернутое описание инструмента и методы-помошники для
   проверки поступающих значений и вывода результата.
 - `ru.yandex.direct.internaltools.core.InternalToolsRegistry` - каталог таких оберток для всех доступных
   инструментов
   
Для использования инструментов в проекте нужно создать каталог и передать его сервису, пример есть в 
`direct/libs-internal/internaltools`.

#### Как создать свой внутренний инструмент?

Описание внутреннего инструмента состоит из двух частей:

 - описания класса с принимаемыми параметрами (должен наследоваться от 
   `ru.yandex.direct.internaltools.core.container.InternalToolParameter`)
 - описания самого инструмента (должен наследоваться от 
   `ru.yandex.direct.internaltools.core.BaseInternalTool`)
 
Допустим, мы хотим сделать инструмент для ручного добавления записей в ppcdict.ssp_platforms. 
В качестве принимаемых параметров у нас будет имя площадки и ее идентификатор (они берутся из БК). 
В качестве вывода - список всех площадок, имеющихся в базе на текущий момент.
Также, предположим, что имя платформы не может быть длиннее, чем 20 символов.

Первым делом опишем ввод:

    @JsonIgnoreProperties(ignoreUnknown = true)
    @ParametersAreNonnullByDefault
    public class NewSspPlatform extends InternalToolParameter {
        @Input(label = "Название платформы", required = true)
        @Text(valueMaxLen = 20)
        private String name;
        
        @Input(label = "ID", description = "Идентификатор платформы в БК", required = true)
        private Long id;
        
        public String getName() {
            return name;
        }
        
        public void setName(String name) {
            this.name = name;
        }
        
        public Long getId() {
            return id;
        }
        
        public void setId(Long id) {
            this.id = id;
        }
    }

Что мы сделали:

- добавили два поля (name и id), а также геттеры и сеттеры для них
- на каждое поле поставили аннотацию `ru.yandex.direct.internaltools.core.annotations.input.Input`. Эта 
  аннотация сообщает о том, что мы хотим получать это поле от клиента. Она обязательна для вводимых полей.
  В ее джавадоках есть список типов данных, с которыми ее можно использовать и перечень всех ее параметров
- в этой аннотации мы оставили значение required=true по умолчанию, оно гарантирует нам, что в поле не будет null
  или пустой строки
- на поле name поставили аннотацию `ru.yandex.direct.internaltools.core.annotations.input.Text` для указания 
  максимальной длины значения. Это гарантирует нам, что строка будет не длиннее 20 символов. В пакете 
  `ru.yandex.direct.internaltools.core.annotations.input` есть несколько таких аннотаций, упрощающих работу файласи, 
  числами, идентификаторами и проч.
- `@JsonIgnoreProperties(ignoreUnknown = true)` добавлен с целью избежать ошибок сериализации в случае, когда от 
  клиента приходят лишние поля. Для сериализации и конвертации параметров в класс мы используем jackson
  
Теперь нам нужно написать сам инструмент:

    @Tool(
            name = "Тестовый инструмент",
            label = "_controller_test_tool",
            description = "Тестовый инструмент для проверки всего на свете",
            consumes = NewSspPlatform.class,
            type = InternalToolType.WRITER
    )
    @Category(InternalToolCategory.SSP_PLATFORMS)
    @Action(InternalToolAction.SET)
    @AccessGroup({InternalToolAccessRole.MANAGER})
    @ParametersAreNonnullByDefault
    public class AddSspPlatformTool extends MassInternalTool<NewSspPlatform, SspPlatformInfo> {
        private static final Logger logger = LoggerFactory.getLogger(AddSspPlatformTool.class);
        
        private final SspPlatformService sspPlatformService;
    
        @Autowired
        public AddSspPlatformTool(SspPlatformService sspPlatformService) {
            this.sspPlatformService = sspPlatformService;
        }
    
        @Override
        public ValidationResult<NewSspPlatform, Defect> validate(NewSspPlatform newSspPlatform) {
            ItemValidationBuilder<NewSspPlatform, Defect> validationBuilder =
                    ItemValidationBuilder.of(newSspPlatform);
    
            validationBuilder
                    .item(newSspPlatform.getId(), "id")
                    .check(greaterThan(0));
    
            return validationBuilder.getResult();
        }
    
        @Override
        protected List<SspPlatformInfo> getMassData() {
            return sspPlatformService.getAllPlatforms();
        }
    
        @Override
        protected List<SspPlatformInfo> getMassData(NewSspPlatform param) {
            logger.info("User {} added {} platform with identifier {}", param.getOperator().getLogin(),
                    param.getName(), param.getId());
            sspPlatformService.addPlatform(param.getName(), param.getId());
            return getMassData();
        }
    }
    
Что мы сделали в этом куске кода:

- с помощью аннотации `ru.yandex.direct.internaltools.core.annotations.tool.Tool` указали, что этот класс - 
  внутренний инструмент. Аннотация обязательна, она наследуется от спрингового компонента и по ней производится
  автоматический поиск всех инструментов. Значения ее параметров можно узнать в джавадоке. Сейчас хочется обратить 
  внимание только на два из них:
  + `consumes = NewSspPlatform.class` сообщает нам, какой класс входящих параметров используется. Именно отсюда
    берется описание класса и генерируются все проверки. Этот класс должен повторять тот, что указан в <>
  + `type = InternalToolType.WRITER` сообщает нам, что инструмент что-то пишет в базу и обращения к нему должны 
    выполняться через POST-запрос. Если его не указать, полезное дествие будет инициироваться через GET, а значит
    будет менее безопасным
- для создания инструмента мы отнаследовались от одного из подклассов `BaseInternalTool`, который предназначен для
  возвращения табличных ответов
- с помощью аннотации `@Category` мы обозначили, к какой категории в общем списке будет относиться инструмент
- с помощью аннотации `@Action` мы обозначили, какую кнопку с призывом к действиям показывать в интерфейсе
- в `@AccessGroup({InternalToolAccessRole.MANAGER})` мы отметили, что доступ к инструменту имеют только менеджеры.
  Если не указывать доступ совсем, то по-умолчанию он будет открыт только для суперов и суперридеров.
  Во всех остальных случаях, когда доступ задается явно, он будет открыт только для тех ролей, которые указаны.
- из всех перечисленных аннотаций только `@Tool` является обязательной
- в методе валидации мы создали новый ItemValidationBuilder, который проверяет, что число больше нуля и, следовательно, 
  может быть идентификатором. При этом мы не проверяем его на null, так как эта проверка была выполнена снаружи, ведь мы
  указали в параметрах, что поле необходимо нам для работы.
- в методе `getMassData`, в логировании мы использовали доступную нам информацию об операторе - пользователе, который
  использовал инструмент
  
Этого кода, в общем случае, достаточно для того, чтобы инструмент появился в интерфейсе и успешно заработал после 
перезапуска приложения

### Где остальной код для использования инструментов в Директе?

- все внутренние инструменты и их конфигурация живут в модуле `direct/libs-internal/internaltools`
- код, отдающий инструменты клиентам в виде JSON-API лежит в `direct/web` в пакете 
  `ru.yandex.direct.web.entity.internaltools`
- код фронтенда находится в ресурсах того же проекта в `direct/web/src/main/resources/webapp/static` 
  + `internal_tools.html` содержит простой загружающий HTML-код
  + `internaltools` - директория с одностраничным react-приложением, занимающимся 
    непосредственно отображением клиентского интерфейса
