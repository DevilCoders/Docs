## Страница Параметров кампании (создания/редактирования и просмотра)

**ТГО**
* [Редактирование](https://9081.beta2.direct.yandex.ru/registered/main.pl?cmd=editCamp&cid=13077378&ulogin=alisecar&retpath=%2Fregistered%2Fmain.pl%3Fcmd%3DshowCamps%26ulogin%3Dalisecar&csrf_token=p_frLY9YpnT_B2TD)
* [Просмотр](https://9081.beta2.direct.yandex.ru/registered/main.pl?cmd=showCampSettings&cid=13077378&ulogin=alisecar&retpath=%2Fregistered%2Fmain.pl%3Fcmd%3DshowCamps%26ulogin%3Dalisecar&csrf_token=p_frLY9YpnT_B2TD)
```
direct-sql dt:ppc:all "SELECT cid FROM campaigns WHERE type = 'text' and statusEmpty != 'yes' ORDER BY cid DESC limit 10"
```

**ДО**
* [Редактирование](https://8080.beta2.direct.yandex.ru/registered/main.pl?cmd=editCamp&cid=114595401&ulogin=krasivoeyabloko&retpath=%2Fregistered%2Fmain.pl%3Fcmd%3Dsearch%26searchcampname%3D%26searchcid%3D114595401%26searchlogin%3D%26searchorderid%3D%26manageruid%3Dany%26who%3Dcamps&csrf_token=R1fS3Wv7ptgdfbd2)
* [Просмотр](https://8080.beta2.direct.yandex.ru/registered/main.pl?cmd=showCampSettings&cid=114595401&ulogin=krasivoeyabloko&retpath=%2Fregistered%2Fmain.pl%3Fcmd%3Dsearch%26searchcampname%3D%26searchcid%3D114595401%26searchlogin%3D%26searchorderid%3D%26manageruid%3Dany%26who%3Dcamps&csrf_token=R1fS3Wv7ptgdfbd2)
```
direct-sql dt:ppc:all "SELECT cid FROM campaigns WHERE type = 'dynamic' and statusEmpty != 'yes' ORDER BY cid DESC limit 10"
```

**РМП**
* [Редактирование](https://8080.beta1.direct.yandex.ru/registered/main.pl?cmd=editCamp&cid=114595386&ulogin=krasivoeyabloko&retpath=%2Fregistered%2Fmain.pl%3Fsearchlogin%3D%26searchorderid%3D%26who%3Dcamps%26cmd%3Dsearch%26manageruid%3Dany%26searchcampname%3D%26searchcid%3D114595386&csrf_token=TAee5zxivBAWLfhF)
* [Просмотр](https://8080.beta1.direct.yandex.ru/registered/main.pl?cmd=showCampSettings&cid=114595386&ulogin=krasivoeyabloko&retpath=%2Fregistered%2Fmain.pl%3Fsearchlogin%3D%26searchorderid%3D%26who%3Dcamps%26cmd%3Dsearch%26manageruid%3Dany%26searchcampname%3D%26searchcid%3D114595386&csrf_token=TAee5zxivBAWLfhF)
```
direct-sql dt:ppc:all "SELECT cid FROM campaigns WHERE type = 'mobile_content' and statusEmpty != 'yes' ORDER BY cid DESC limit 10"
```

**СМАРТ**
* [Редактирование](https://9081.beta2.direct.yandex.ru/registered/main.pl?cmd=editCamp&cid=25990792&ulogin=tj1-04&retpath=%2Fregistered%2Fmain.pl%3Fmanageruid%3Dany%26searchcid%3D25990792%26searchorderid%3D%26searchcampname%3D%26who%3Dcamps%26searchlogin%3D%26cmd%3Dsearch&csrf_token=MI0I9Jsd8oJofZvt)
* [Просмотр](https://9081.beta2.direct.yandex.ru/registered/main.pl?cmd=showCampSettings&cid=25990792&ulogin=tj1-04&retpath=%2Fregistered%2Fmain.pl%3Fmanageruid%3Dany%26searchcid%3D25990792%26searchorderid%3D%26searchcampname%3D%26who%3Dcamps%26searchlogin%3D%26cmd%3Dsearch&csrf_token=MI0I9Jsd8oJofZvt)
```
direct-sql dt:ppc:all "SELECT cid FROM campaigns WHERE type = 'performance' and statusEmpty != 'yes' ORDER BY cid DESC limit 10"
```

**Медийно-контекстный баннер на поиске (новый баян)**
* [Редактирование](https://8080.beta1.direct.yandex.ru/registered/main.pl?cmd=editCamp&cid=91508951&ulogin=allpianosru&retpath=%2Fregistered%2Fmain.pl%3Fulogin%3Dallpianosru%26csrf_token%3DPlzLDzvBkuZkdoQM%26cmd%3DshowCamps&csrf_token=_ASqivgogyqmLuWT)
* [Просмотр](https://8080.beta1.direct.yandex.ru/registered/main.pl?cmd=showCampSettings&cid=91508951&ulogin=allpianosru&retpath=%2Fregistered%2Fmain.pl%3Fulogin%3Dallpianosru%26csrf_token%3DPlzLDzvBkuZkdoQM%26cmd%3DshowCamps&csrf_token=_ASqivgogyqmLuWT)
```
direct-sql dt:ppc:all "SELECT cid FROM campaigns WHERE type = 'mcbanner' and statusEmpty != 'yes' ORDER BY cid DESC limit 10"
```

**Баннеры в сетях (охватный продукт)**
* [Редактирование](https://8080.beta1.direct.yandex.ru/registered/main.pl?cmd=editCamp&cid=115368441&ulogin=krasivoeyabloko&retpath=%2Fregistered%2Fmain.pl%3Fsearchorderid%3D%26searchcampname%3D%26searchcid%3D115368441%26who%3Dcamps%26searchlogin%3D%26manageruid%3Dany%26cmd%3Dsearch&csrf_token=k_mYe5eZVjfJ08k6)
* [Просмотр](https://8080.beta1.direct.yandex.ru/registered/main.pl?cmd=showCampSettings&cid=115368441&ulogin=krasivoeyabloko&retpath=%2Fregistered%2Fmain.pl%3Fsearchorderid%3D%26searchcampname%3D%26searchcid%3D115368441%26who%3Dcamps%26searchlogin%3D%26manageruid%3Dany%26cmd%3Dsearch&csrf_token=k_mYe5eZVjfJ08k6)
```
direct-sql dt:ppc:all "SELECT cid FROM campaigns WHERE type = 'cpm_banner' and statusEmpty != 'yes' ORDER BY cid DESC limit 10"
```
