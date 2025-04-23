Пара кнопок "назад-вперед" для ротации какого то произвольного содержимого.

Пример:

    ...
    onSetMod: {
        js: function() {
            var rotateButtons = this.findBlockOn('rotate-buttons', 'b-rotate-buttons');

            rotateButtons.on('back next', function(e) {
                console.log('walk ', e.type);
            });

            // По умолчанию ограничений на цикличность ротации не наложено,
            // но можно ограничить, допустим 5 элементами
            // В таком случае, при достижении границ соотв. кнопки будут блокированы.
            rotateButtons.setSize(5);

            // API блока предусматривает программную навигацию
            // вперед
            rotateButtons.goNext()

            // и назад
            rotateButtons.goBack();

            // Допускается блокировка блока, при которой вся пара кнопок будет выключена
            rotateButtons.setMod('disabled', 'yes');
        }
    }
    ...
