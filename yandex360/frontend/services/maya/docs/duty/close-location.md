# Закрытие локаций

По договорённости с дежсменой, есть несколько случаев, когда требуется закрывать локацию (гасить инстансы приложения в одном из ДЦ) во избежание проблем, связанных с бекендами и/или частичной связностью.
- Глобальные проблемы, про которые точно известно, что они локализуются до одного ДЦ - **закрывает дежсмена**
- Регламентные работы, проводящиеся на одном ДЦ - **закрывает дежсмена**
- Общие учения (закрытие локации глобально, на уровне маршрутизации/HBF/whatever_else) - **закрывает дежсмена**
- Локальные учения (календарные/почтовые) - **закрываем сами**


Чтобы закрыть локацию, требуется выполнить в executer:
```bash
# <loc> - краткое имя ДЦ (sas/iva/vla/man/myt)
p_exec %mail_maya_production_maya@<loc> supervisorctl stop nginx
p_exec %mail_maya-corp_production_maya@<loc> supervisorctl stop nginx
```
Чтобы открыть локацию, требуется выполнить в executer:
```bash
# <loc> - краткое имя ДЦ (sas/iva/vla/man/myt)
p_exec %mail_maya_production_maya@<loc> supervisorctl start nginx
p_exec %mail_maya-corp_production_maya@<loc> supervisorctl start nginx
```