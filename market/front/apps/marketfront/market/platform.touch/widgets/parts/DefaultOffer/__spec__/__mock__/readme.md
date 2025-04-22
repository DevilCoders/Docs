
### Как удобно собрать моки

пишу для облегчения обновления моков (вручную их исследовать/собирать считаю оверхедным).

моки собирал так:

в контроллере вставляем
```angular2html
import fs from 'fs';

const dirPath = "/home/dmbaranov/marketfront_dmbaranov/market/platform.touch";

const errFunc = (err) => {
    if (err) {
        return console.log('fs.writeFile err', err);
    }
}

productPromise.then(res => {
    fs.writeFile(`${dirPath}/productPromise.txt`, JSON.stringify(res), errFunc);
});
defaultOfferPromise.then(res => {
    fs.writeFile(`${dirPath}/defaultOfferPromise.txt`, JSON.stringify(res), errFunc);
});
pageStatePromise.then(res => {
    fs.writeFile(`${dirPath}/pageStatePromise.txt`, JSON.stringify(res), errFunc);
});
```


после, со стенда файлы моков можем вытянуть по ssh:
```angular2html
scp logrus02vd.market.yandex.net:/home/dmbaranov/marketfront_dmbaranov/market/platform.touch/productPromise.txt ./productPromise.txt
scp logrus02vd.market.yandex.net:/home/dmbaranov/marketfront_dmbaranov/market/platform.touch/pageStatePromise.txt ./pageStatePromise.txt
scp logrus02vd.market.yandex.net:/home/dmbaranov/marketfront_dmbaranov/market/platform.touch/defaultOfferPromise.txt ./defaultOfferPromise.txt
```



### коммент при запуске testament (важно)
Не забудь поменять конфиг репорта/бекендов на тестовый перед запуском тестамента
(тестамент на конфиге от прода будет просто до таймаута висеть)
