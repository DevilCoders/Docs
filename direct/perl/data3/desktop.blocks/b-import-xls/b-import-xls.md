#b-import-xls#

##Описание##
Блок с интерфейсом загрузки кампаний из XLS/XLSX

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[kabzon](https://staff.yandex-team.ru/kabzon)

###Где используется###

* `p-xls-management` - как контент вкладки импорта кампаний на странице управления кампаниями с помощью XLS/XLSX

##Roadmap & known issues##

* код блока очень старый, можно разделить его, вынеся часть во view-модель
* нужно переписать блок с bemtree на bemhtml
* упростить декларацию блока, сведя к минимуму набор входных параметров (причины см. в примере ниже)

##Пример##

```

    {
        block: 'b-import-xls',
        action: this.data.script,
        agencies: this.data.for_agencies,
        allow: {
            createBySubclient: this.data.allow_create_scamp_by_subclient,
            createCampaign: !hasLoginRights('support_control', 'media_control'),
            loadToMediaPlan: hasLoginRights('super_control', 'media_control')
        },
        service: {
            bySelf: hasLoginRights('is_any_client', 'super_control', 'support_control'),
            byManager: hasLoginRights('manager_control')
        },
        notAgencyControl: !hasLoginRights('agency_control'),
        isAnyClient: hasLoginRights('is_any_client'),
        hasMediaControl: hasLoginRights('media_control'),
        hasSupportControl: hasLoginRights('support_control'),
        campaign: {
            geo: 0,
            geoText: u.getGeoNames(0)
        },
        formProperties: {
            cmd: 'importCampXLS',
            ulogin: this.data.user_login,
            retpath: decodeURIComponent(u.getCurrentUrl()),
            svars_name: ''
        },
        uploadProperties: {
            cmd: 'preImportCampXLS',
            ulogin: this.data.user_login,
            import_format: 'xls',
            json: 1
        },
        campaigns: this.data.camps_name_only.filter(function(campaign) {
            return !campaign.mediaType;
        }),
        campLimitError: this.data.camp_limit_error
    }
```
