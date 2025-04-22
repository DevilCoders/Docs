## Полезные алиасы
```
alias cdwork='cd ~/arc/arcadia/market/project'
alias arc_mount='cd ~/arc && arc mount -m arcadia/ -S store/ && cdwork'
alias arc_unmount='cd ~ && arc unmount'
alias ya_idea='ya ide idea -l --group-modules=tree --iml-in-project-root -r .'
alias ya_stylecheck='ya make -tF *::jstyle'
```

Для создания постоянных алиасов, которые не будут удаляться после перезагрузки терминала, необходимо записать их в специальный скрытый файл: 
* ``` ~/.bashrc ``` (для Linux)
* ```~/.bash_profile``` или ```~/.zshrc``` (для MacOS).
