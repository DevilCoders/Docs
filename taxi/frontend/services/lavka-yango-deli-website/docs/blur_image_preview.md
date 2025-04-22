# Блур изображения при загрузке страницы

1. Установить библиотеку SQIP https://github.com/axe312ger/sqip с необходимыми плагинами:
   ```bash
   npm install sqip@canary sqip-plugin-primitive@canary sqip-plugin-svgo@canary sqip-plugin-data-uri@canary
   ```
2. Добавить в любую асинхронную функцию следующий код:
   ```ts
    import sqip, {resolvePlugins} from 'sqip';
    try {
        const result = await sqip({
            input: /* Асболютный путь к изображению */
        });
        console.debug(result);
    } catch (err) {
        console.error(err);
    }
   ```
3. В консоли сервера выведется информация об изменном изображении, например:
   ```bash
   {
       content: Buffer.from('<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 300 188">...</svg>'),
       metadata: {
           originalWidth: 1024,
           originalHeight: 640,
           palette: {
           Vibrant: Vibrant.Swatch,
           DarkVibrant: Vibrant.Swatch,
           LightVibrant: Vibrant.Swatch,
           Muted: Vibrant.Swatch,
           DarkMuted: Vibrant.Swatch,
           LightMuted: Vibrant.Swatch
       },
       width: 300,
       height: 188,
       type: 'svg',
       // These will be added by sqip-plugin-data-uri
       dataURI: "data:image/svg+xml,...",
       dataURIBase64: 'data:image/svg+xml;base64,...'
      }
   }
   ```
   Интересующий параметр - dataURI, нужно его скопировать

4. Добавить скопированный dataURI в background-image контейнера изображения, например:
   ```css
   background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 300 167'%3e%3cdefs/%3e%3cfilter id='a'%3e%3cfeGaussianBlur stdDeviation='55'/%3e%3c/filter%3e%3crect width='100%25' height='100%25' fill='%23423328'/%3e%3cg filter='url(%23a)'%3e%3cg fill-opacity='.5' transform='translate(.6 .6) scale(1.17188)'%3e%3ccircle r='1' fill='%23e9d483' transform='matrix(32.7843 117.47468 -94.3028 26.3176 141.6 104)'/%3e%3cellipse cx='167' cy='29' fill='%2326243c' rx='47' ry='37'/%3e%3cellipse cx='89' cy='27' fill='%23dad4d1' rx='28' ry='54'/%3e%3ccircle r='1' fill='%23f8cb2c' transform='matrix(-10.91413 58.77975 -60.7003 -11.27074 108.4 120)'/%3e%3cpath d='M72.3 80.2l51 3.6-1.6 22-51-3.6z'/%3e%3cpath fill='%23000007' d='M8 0h54v69H8z'/%3e%3cellipse cx='216' cy='114' fill='%235f6274' rx='47' ry='115'/%3e%3ccircle cx='54' cy='87' r='17' fill='%23ff0'/%3e%3c/g%3e%3c/g%3e%3c/svg%3e");
    ```
5. При необходимости добавить следующие стили в тот же контейнер:
   ```css
   background-size: cover;
   background-repeat: no-repeat;
   ```

6. При необходимости повторить пункт 4 для других изображений, заменяя только путь к изображению в пункте 2.
7. Удалить код из пункта 2, удалить библиотеку:
   ```bash
   npm uninstall sqip-plugin-primitive sqip-plugin-svgo sqip-plugin-data-uri  --save-dev
   ```
