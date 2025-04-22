#Добавление новых утилит в i-utils#

##UPD: теперь процесс упростился за счет создания технологии utils.js##

Теперь для того, чтобы добавить какие-то новые утилиты, нужно выполнить следующее:

* Создать в `direct-utils/adv-blocks/i-utils` новый элемент, например `__cool-utils`
* В папке `__cool-utils` создать файл: `i-utils__cool-utils.utils.js`
* В файле `i-utils__cool-utils.utils.js` написать реализацию ваших утилит и зарегистрировать их через `u.register()`, например:


    u.register({ 
        coolFunc: function() { 
            console.log('hello') 
        }
    });

* Все. Этот код выполнится как на клиенте, так и bemtree-шаблоне. Все зарегистрированные функции будут доступны через %%u.имя_функции%% (например, %%u.coolFunc%%)

##Способ ниже устарел, но также работоспособен##
Для того, чтобы добавить какие-то новые утилиты, нужно выполнить следующее:

* Создать в `direct-utils/adv-blocks/i-utils` новый элемент, например `__cool-utils`
* В папке `__cool-utils` создать два файла: `i-utils__cool-utils.js` и `i-utils__cool-utils.bemtree.xjst`
* В файле `i-utils__cool-utils.js` написать реализацию ваших утилит и зарегистрировать их через `u.register()`, например:


    u.register({ 
        coolFunc: function() { 
            console.log('hello') 
        }
    });

* После этого все зарегистрированные функции будут доступны на **клиентских** шаблонах через %%u.имя_функции%% (например, %%u.coolFunc%%)
* В файле %%i-utils__cool-utils.bemtree.xjst%% написать следующее (заменив имя элемента на ваше): 

    block i-utils, default, this.utilsElem: {

        (new Function('borschik:include:../../libs/adv-blocks/i-utils/__cool-utils/i-utils__cool-utils.js'))
                .call(this);

        applyNext(this.utilsElems = true);
    }

* После этого все зарегистрированные функции будут доступны на **серверных** шаблонах через %%u.имя_функции%% (например, %%u.coolFunc%%)