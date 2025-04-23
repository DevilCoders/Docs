# Общий конфиг для компоненты
Раздел находится в разработке, и пока не имеет ничего общего с реальным положением дел.
Все внутренние классы можно будет легко переделать в dataclasses при внедрении третьего питона везде.
В классе конфига хочется описать все "чистые" параметры и функции, а всю логику вынести в helpers
```python
class MyBranchedComponent(ReferenceBranchedConfig):
    """ Компонента с релизным циклом из бранчей и тегов """
    name = "my_component"  # [Obligatory] Имя-идентификатор компоненты. Желательно маленькими буквами и через нижнее подчеркивание
    display_name = u'My Component'  # [Optional] Человеко-читаемое название компоненты на английском языке, с большой буквы. По-умолчанию = u" ".join(p.capitalize() for p in self.name.decode("utf-8").split("_"))

    class SvnCfg(ReferenceBranchedConfig.SvnCfg):
        ARCADIA = "arcadia:/"
        REPO_NAME = "arc"
        repo_base_url = ARCADIA + REPO_NAME
        main_url = None

    class Releases(ReferenceBranchedConfig.Releases):
        kpi_alert = 7
        responsible = "pupkin"  # [Obligatory] Ответственный за релиз, указывается логин со стаффа конкретного человека.
        resources_info = [
            ReleasedResourceInfo("name1", "resource_name1", "build_ctx_key", ["roll_with1"]),
            ReleasedResourceInfo("name2", "resource_name2", "build_ctx_key", ["roll_with2"]),
        ]  # [Optional]
        release_followers_permanent = []

        def release_notes(self, **kwargs):  # Stable, testing, unstable, prestable
            pass

    class ReleaseViewer(object):
        check_service = {}
        kpi_alert = 0
        kpi_alerts_recipients = None

    class Testenv(object):
        allowed_dbs = ("my_component-[0-9]+",)  # [Optional] По-умолчанию: ("ws-{}-[0-9]+", "{}-[0-9]+")
        trunk_task_owner = "AB-TESTING"  # [Obligatory] Owner sandbox-задач в транковой базе
        branch_task_owner = "AB-TESTING"  # [Optional] Owner sandbox-задач в клонированных базах. По-умолчанию: self.trunk_task_owner
        trunk_db = "my_component-trunk"  # [Optional] Транковая база в тестенве. По-умолчанию: self.name + "-trunk"
        branch_db_template = "my_component-{testenv_db_num}"  # [Optional] Шаблон для клонированной базы в тестенве
        each_rev_default = False
        last_good_revision_ignore_release_jobs = False  # ??? Понять что это и переименовать

        def add_databases(self, **kwargs):
            """ Нужно для базового и rtyserver """
            pass

        def add_jobs(self, **kwargs):
            """ Нужно для базового и rtyserver """
            pass

        def db_stop_range(self, branch_number):
            pass

        def db_drop_range(self, branch_number):
            pass

        class JobPatch(ReferenceBranchedConfig.Testenv.JobPatch):
            @property
            def change_frequency(self):
                custom_change = super(MyBranchedComponent.Testenv.JobPatch, self).change_frequency
                custom_change.update({"_{}_QUALITY_ACCEPTED".format(self.name): rm_const.TestFrequencies.LAZY_TEST})
                return custom_change

            @property
            def ignore_match(self):
                return super(MyBranchedComponent.Testenv.JobPatch, self).ignore_match + [
                    "MERGE_FUNCTIONAL",
                    "ROLLBACK_TRUNK_AND_MERGE_FUNCTIONAL",
                    "ROLLBACK_TRUNK_FUNCTIONAL",
                ]

    class ChangelogCfg(ReferenceBranchedConfig.ChangelogCfg):
        wiki_page = "my/wikipage/url/"  # [Obligatory]
        wiki_page_owner = "pupkin"
        wiki_head_template = "===={descr} //r:{r1}-{r2}//\nCreation date: {date}"
        review_groups = ["my_component_review_group"]  # [Optional]
        markers = None  # [Optional]
        observed_paths = ["arcadia/my_component/dir1", "arcadia/my_component/dir2"]  # [Optional]
        ya_make_targets = ["arcadia/my_component/dir3"]  # [Optional]
        svn_paths = []
        svn_paths_banned = []

    class Yappy(ReferenceBranchedConfig.Yappy):
        """ Придумать как он должен выглядеть """
        betas = {
            # beta_conf_type - идентификатор типа беты, произвольная строка, должна передаваться в параметре
            # beta_conf_type в задаче генерации беты (GENERATE_YAPPY_BETA) и запуска серпов (LAUNCH_METRICS)
            # если не указана sample_beta
            "beta_conf_type":
                configs.YappyTemplateCfg(  # Есть 2 типа бет, первый - заданный в яппи через yappy/data/templates
                    template_name="template_name",  # Название template-a
                    working_betas_limit=3,  # Допустимое количество одновременно запущеных бет данного типа
                    patches=[
                        configs.YappyTemplatePatch(
                            patch_dir="patch_dir",  # Директория, в которой должны лежать патчи для указанного шаблона
                            resources=[  # Информация о ресурсах в патче
                                configs.YappyParametrizedResource(  # Параметризованный тип ресурса, должен передаваться
                                # через параметры в задаче генерации бет
                                    local_path="local_path",  # localPath для ресурсов в патче
                                    param_name="res_id_param",  # Название параметра из которого брать ресурс для патча
                                    checkconfig_name="checkconfig_name",  # [Optional] добавить в патч информацию
                                    # expectedCheckconfig, <checkconfig_name>=<expected_resource_md5>
                                    storage="storage_type"  # [Optional] добавить для ресурса storage=<storage_type>
                                ),
                                configs.YappyStaticResource(# Ресурс-константа, задается в конфиге и не меняется через
                                #  параметры задачи генерации бет
                                    local_path="local_path_2",
                                    manage_type="manage_type",  # manageType для ресурса, например "DELETED",
                                    # "BC_DEFAULT", SANDBOX_RESOURCE, STATIC_CONTENT
                                    resource_id = resource_id,  # [Optional] id ресурса, указывается для
                                    # manage_type="SANDBOX_RESOURCE"
                                    content = content,  # [Optional] Контент ресурса беты, указывается для
                                    # manage_type="STATIC_CONTENT"
                                ),
                                YappyLastReleasedResource(  # Ресурс из последней stable released задачи
                                    local_path="local_path_3",
                                    res_type="res_type",  # Последний релиз какого ресурса искать
                                ),

                            ],
                            parent_service="service_name",  # [Optional] поставить parentExternalId в патч
                            ignore_instance_spec=False,  # [Optional] поставить ignoreParentInstanceSpec в патч
                        ),
                    ],
                ),
            "beta_conf_2": yappy_cfg.YappyBetaCfg(  # Бета созданная через yappy/data/betas
                beta_name="beta_name", # Название файла беты в yappy/data/betas
                patches=[
                    configs.YappyBetaPatch(
                        patch_file="patch_file", # Название файла с патчем, где должны лежать патчи указанной беты
                        # (без расширения)
                        resources=[],  # Остальные настройки в YappyBetaPatch идентичны YappyTemplatePatch
                        parent_service="",
                        ignore_instance_spec=False,
                    ),
                ],
            ),
        }
        working_betas_limit = 3

    class MetricsCfg(ReferenceBranchedConfig.MetricsCfg):
        limit_s = 50400  # 14 hours
        default_launch_id = ""

    class Notify(object):  # Класс для конфигурации оповещений о компоненте
        class Mail(ReferenceBranchedConfig.Notify.Mail):
            mailing_list = ["pupkin@yandex-team.ru"]
            def branch_letter(self, **kwargs):
                pass

        class Telegram(ReferenceBranchedConfig.Notify.Telegram):
            chats = ["my_component"]  # Список Telegram-чатиков, прописанных в projects/release_machine/rm_notify.py

        class Startrek(ReferenceBranchedConfig.Notify.Startrek):
            assignee = "pupkin"  # Первоначальный исполнитель приемочных тикетов Startrek
            use_task_author_as_assignee = True
            add_commiters_as_followers = True
            nanny_reports = True
            queue = "YOURQUEUE"  # Очередь, в которой заводится тикет в трекере
            followers = ["pupkin", "dudkin"]  # [Optional] Кого добавляем в наблюдатели тикета
            components = u"Моя компонента".encode('utf-8')  # [Optional] Имя компоненты для поля components тикета в трекере
            workflow = rm_const.Workflow.BETA_TEST  # [Optional] Последовательность статусов релизного тикета. Релизная машина умеет менять статус тикета в зависимости от стадии. По-умолчанию = {}.
            summary_template = u"Приемка моей компоненты {}"  # Шаблон для заголовка тикета в трекере
            deadline = 3
            banned_queues = {"IGNIETFERRO"}
            write_merges_in_table = True

            @property
            def banned_people(self):
                return super(self.__class__, self).banned_people | {"additional_logins"}
 ```

## Проблемы
Логика, различная для разных компонент
```python
class Metrics(object):
    """ Люди могут захотеть делать """
    # todo: положить в StartrekNotifyConfig?
    launch_result_on_start = "???"
    launch_result_in_middle = "???"
    launch_result_on_end = "???"

```
