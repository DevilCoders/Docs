[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/cilt)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/cilt) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/cilt)](https://oko.yandex-team.ru/pkg/@yandex-market/cilt)

Сilt - CLI Toolset
===========

Очень быстрый микрофреймворк для построения CLI приложений. 
Основное внимание уделено автогенерации справки, простоте описания автодополнения и валидации параметров

Пример оформления файла с командой:

```(javascript)
module.exports = {
    name: "start",
    description: "Запустить сервер",
    args: [
        {
            name: "server",
            description: "Название пакета с сервером",
            longDescription: "Название пакета в большинстве случаев совпадает с директорией, однако это не является обязательным правилом. Название пакета указываается в соответствующем package.json в поле name. Для получения списка всех пакетов с их описанием используйте 'yammy list'",
            choices: async function packages() {
                const repo = require("../models/repo");
                const packages = await repo.packages();

                const hasServer = await Promise.all(packages.map(async function(pkg) {
                    const hasServer = await pkg.server.hasServer();
                    return {pkg, hasServer};
                }));

                return hasServer
                    .filter(function({hasServer}) { return hasServer; })
                    .map(function({pkg}) { return pkg.name; });
            }
        }
    ],
    handler: function({server}) {
        const Pkg = require("../models/pkg");
        const pkg = Pkg.factory(server);
        return pkg.server.start();
    }
};

```

**TODO** Написать документацию
