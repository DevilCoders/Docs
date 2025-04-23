# pixel

Пиксель - скрипт для сбора аудитории и отслеживания конверсии. По причинам безопасности, такие скрипты можно использовать только внутри iframe.

Ипользуются [MT](https://target.my.com/help/advertisers/sourcetopmailru/ru) и [VK](https://vk.com/faq12142).

## Как изменять
Обновить содержимое папки ./iframe_sources. Залить на [s3](https://yc.yandex-team.ru/folders/fooh84tm1kfqblnmotsd/storage/buckets/tuning?key=partner_frame%2F). js нужно загружать вместе с gzip и br версиями (`brew install brotli` - скачать brotli)
`brotli file.svg -> file.svg.br gzip file.svg -> file.svg.gz`

## Как использовать
### Инициализация
```
import {
    initPixel,
    iframeId,
    getIframeUrl
} from '@ps-int/ufo-rocks/lib/helpers/pixel';

interface PixelIframeProps {
    vkId: string;
    mtId: string;
}
// id пикселя и счётчика берутся в личных кабинетах вк и мт
const PixelIframe = ({ vkId, mtId }: PixelIframeProps) => {
    const iframeSource = getIframeUrl({ vkId, mtId });

    useEffect(() => {
        initPixel();
    }, []);

    return (
        <iframe
            id={iframeId}
            style={{ display: 'none' }}
            src={iframeSource}
        />
    );
};
```
### Отправка событий
```
import { sendPixelMessage, PixelTypes } from '@ps-int/ufo-rocks/lib/helpers/pixel';
...
sendPixelMessage({
    pixelType: PixelTypes.vk,
    goal: 'purchase',
    value: 123
});
sendPixelMessage({
    pixelType: PixelTypes.mt,
    goal: 'purchase',
    value: 123
});
```
