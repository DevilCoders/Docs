## Наноблок `nb-resource` со значением type='audio'

## JS API

```
var resource = nb.block(nodeResourse);

/**
 * setPlaying
 */
resource.setPlaying(true); // - добавить состояние проигрывания
resource.setPlaying(false); // - снять состояние проигрывания

/**
 * setPaused
 */
resource.setPaused(true); // - добавить состояние паузы
resource.setPaused(false); // - снять состояние паузы

/**
 * updateProgress
 */
resource.updateProgress(30); // - установить прогресс в 30%

/**
 * updateTimeCurrent
 */
resource.updateTimeCurrent(12); // установить текущее время - 12 секунд - значение форматируется

/**
 * updateTimeTotal
 */
resource.updateTimeTotal(123); // - установить общее время - 123 секунды - значение форматируется

```