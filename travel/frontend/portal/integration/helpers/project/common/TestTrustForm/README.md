### Заполнение формы оплаты

Метод который заполняет форму оплаты и нажимает кнопку "Оплатить".

Нужно чтобы страница с формой находилась в "фокусе" экземпляра браузера.
У нас страница с оплатой встроена в приложение в `<iframe>`,
поэтому перед вызовом метода нужно "сфокусироваться" на этот `iframe`.

Пример теста:

```
it('some test with trust form', async function() {
        // ...
        // некоторые действия приводящие на url страницы с оплатой

        /*
        Получаем iframe с формой оплаты.
        Здесь для простоты приведен пример с селектором,
        но предпочтителен способ через pageObject и QA атрибуты
        */
        const iframeSelector = 'iframe';
        await this.browser.waitForExist(iframeSelector);
        const frame = await this.browser.$(iframeSelector);

        await this.browser.switchToFrame(frame);

        await pay(this.browser);

        await this.browser.switchToParentFrame();

        // ...
    });

```
