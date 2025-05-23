# Совместное редактирование документов

В Office 365 есть возможность совместного редактирования документов Word, Excel и PowerPoint: несколько пользователей могут одновременно вносить в документ изменения и сохранять их. Эта возможность работает и для облачных документов, встроенных на вики-страницы: при редактировании облачный документ открывается в приложении Office 365, и вы можете редактировать его одновременно с другими пользователями.

## Редактировать документ, встроенный на вики-страницу {#edit-button}

Чтобы редактировать документ Office 365, встроенный на вики-страницу, в правом верхнем углу нажмите кнопку **Редактировать в облаке**. Документ откроется в приложении Office 365 в новой вкладке.

Если у вас нет прав на редактирование документа, вы увидите сообщение «У вас нет доступа к этой странице». Чтобы запросить доступ к документу у его автора, введите сообщение и нажмите кнопку **Запрос на доступ**. 

{% note alert %} 

Чтобы редактировать документы, вы должны быть [авторизованы на портале office.com](ms-office.md#office-login). Если у вас нет лицензии Office 365, отправьте запрос через [форму](https://help.yandex-team.ru/?form=soft).

{% endnote %}


### Как перейти на совместное редактирование документов с помощью {{wiki-name}} {#shared-edit}

При подготовке документов часто нужна возможность параллельно вносить исправления или получать комментарии от нескольких коллег.

Раньше можно было пересылать документ друг другу по почте, а потом сводить вместе правки из нескольких версий документа. Или можно было создать страницу на {{wiki-name}} и вносить изменения по очереди.

Теперь есть возможность встроить облачные документы на {{wiki-name}} и редактировать их одновременно с коллегами: 

* Если у вас уже есть документы Office 365, которые вы редактируете вместе с коллегами, вы можете продолжить работу на {{wiki-name}}. Для этого создайте страницу типа **Word, Excel, PowerPoint** и [импортируйте ваш файл](create-ms-office.md#import-doc).

* Если вы совместно с коллегами редактируете страницу на {{wiki-name}}, [создайте новый облачный документ](create-ms-office.md#new-from-wiki) и скопируйте в него текст страницы.

### Как совместно редактировать документы с внешними пользователями {#shared-edit-ext}

Если вам часто нужно работать над документами вместе с контрагентами, которые не являются сотрудниками Яндекса, вы можете предоставить им доступ для совместного редактирования документов в Office 365. Так как доступ внешних пользователей на общий сайт Sharepoint запрещен политиками безопасности, вам потребуется создать отдельный сайт (раздел) в Sharepoint, к которому будет разрешен доступ извне компании. 

Для этого:
1. Напишите письмо на рассылку `help@yandex-team.ru` с просьбой создать для вашей команды или отдела новый сайт Sharepoint, на котором можно будет делиться документами с внешними пользователями. В письме поясните, зачем вам нужна такая возможность.

1. После того как сотрудники HelpDesk создадут для вас сайт, вы сможете [создавать в нем новые документы](create-sharepoint.md#create-sharepoint) или [переместить существующие документы](doc-access.md#move-doc) из других разделов Sharepoint.

1. Чтобы пригласить внешних пользователей для совместного редактирования документов:
   1. Найдите документ на вашем сайте Sharepoint, куда разрешен доступ внешних пользователей.
   1. Наведите указатель на документ, нажмите значок ![](../../_assets/wiki/share-opt.png) и выберите **Управление доступом**.
   1. На открывшейся панели в блоке **Прямой доступ** ведите почтовый адрес внешнего пользователя, которому нужно дать доступ к документу, и выберите уровень доступа **Может изменять**.
   1. Нажмите кнопку **Предоставление доступа**.
   1. Пользователь получит на указанный почтовый адрес письмо со ссылкой. После перехода по ссылке пользователь получит по почте код, который потребуется ввести для доступа к документу.