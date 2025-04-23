***Токен*** - последовательность подряд идущих символов в сообщении.

***Последовательность токенов*** - Последовательность подряд идущих токенов.

***Сообщение*** - Сущность которая обладает следующими составляющими:
 
* Html тело
* Тема письма
* Отправитель

***Шаблон*** - Последовательность последовательностей токенов которая является общей в некотором множестве писем. 
Между двумя подряд идущими токенами находится **дельта**, также она располагается перед первым токеном, и после последнего.
<details><summary><b>Example:</b></summary><p>

```json
 [
 ['\n', '<html>', '<body>', '\n', '<h2>'],
 ['</a>', '</h2>', '\n', '<p>'],
 ['</p>', '\n', '<p>'],
 ['Поздравления можно направлять по адресу '],
 ['</a>'],
 ['</p>', '\n', '<p>', '<br />', '\n'],
 ['<br />', '\n', '<br />', '\nЭто сообщение отправлено из '],
 ['Мегаплана', '</a>', '. Отказаться от\nуведомлений можно в '],
 ['настройке\nподписки', '</a>', '.', '</p>', '\n', '</body>', '</html>','\n']
 ]
```

</p></details>

***Длина шаблона*** - количество **последовательностей токенов** в **шаблоне**, для предыдущего примера, длина шаблона равна 9.

***Дельта*** - Последовательность последовательностей токенов. Каждая последовательность токенов располагается между 
соседними последовательностями токенов в **шаблоне**, соответственно после добавления дельты в соответствующие пропуски
в шаблоне мы получим изначальное сообщение. 
Длина дельты вычисляется как **длина шаблона** + 1.
<details><summary><b>Example:</b></summary><p>

```json
  [
  [],
  ['Вам начисление 777$ Иван Игнатьевич, Подтвердите получение'],
  ['Здравствуйте Иван Игнатьевич!'],
  ['Иван Игнатьевич, только сегодня хочу вам предложить новый способ заpaботка стоимостью'],
  ['<a href="https://petrbiz.justclick.ru/lms/api-login/?_hash=zIj%2BCy3L65kRdtL4DE3r508BT12id4awSHpvMkkLY4c%3D&amp;authBhvr=1&amp;email=ivedyakin%40mail.ru&amp;expire=1574174180&amp;lms%5BrememberMe%5D=1&amp;targetPath=https%3A%2F%2Fpetrbiz.justclick.ru%2Ftrack%2F708043696%2Fanons%2F1200502868%2Fhttp%25253A%25252F%25252Fnacho3131.blogspot.com%25252F%25253Furl%25253Do281%3F_hash%3DqQscngnfyDUmLYWci%252B7BtDk3VH%252FIfMowEA3hVQsJBX0%253D">'],
  ['<img src="https://petrbiz.justclick.ru/mailview/a/1200502868/708043696/" />'],
  ['<a href="petrbiz.justclick.ru">', 'justclick.ru'],
  ['<a href="https://petrbiz.justclick.ru/lms/api-login/?_hash=UpmwyC18f3yi4ERPcgs7XxOBW6K0PNYnE44Z7EXdOvE%3D&amp;authBhvr=1&amp;email=ivedyakin%40mail.ru&amp;expire=1574174180&amp;lms%5BrememberMe%5D=1&amp;targetPath=https%3A%2F%2Fpetrbiz.justclick.ru%2Fsubscr%2Fin%2F%3Fsid%3D20634df6%26crc%3D6ce35f235b68470cd59930fe67db69a17ff80c933db0a13c762106f1a01ff996" title="Все ваши письма отправленные сервисом justclick.ru">'],
  ['<a href="petrbiz.justclick.ru">', 'petrbiz.justclick.ru'],
  ['<a href="https://petrbiz.justclick.ru/lms/api-login/?_hash=PxJrzvLo0MfBYIODKCQ6rytkp%2BGprjB7NXTmngOqTL4%3D&amp;authBhvr=1&amp;email=ivedyakin%40mail.ru&amp;expire=1574174180&amp;lms%5BrememberMe%5D=1&amp;targetPath=https%3A%2F%2Fpetrbiz.justclick.ru%2Funsub%2F20634df6%2Fa%2Fee2c1039%2F">'],
  ['Петр\n'],
  []
  ]
```
</p></details>

***Stable sign*** - Хеш функция от сконкатенированных токенов шаблона. На данный момент мы вычисляем md5 и конечный хеш 
является int64_t. **stable sign**  уникальный идентификатор для шаблона, он совпадает если два шаблона одинаковые, 
и не совпадают если есть какие-либо различия.

***LCS*** - longest common subsequence. Используется для нахождения общей части для двух сообщений.

***Message/Template Digest*** - Массив int32_t. Каждый элемент которого это хеш от соответствующего токена **сообщения**/**шаблона**.

***Message/Template Filtered Digest*** - Массив int32_t из которого выброшены все высокочастотные токены. 
Длина filtered digest всегда меньше или равна чем длина обычного digest.

***Detemple Result*** - Ответ сервиса который содержит информацю о статусе операции и имеет одно из следующих значений
```cpp
enum class TDetempleStatus {
    FoundInDb,
    FoundPreparedInPool,
    FoundNotReadyInPool,
    NotFound,
    Error
};
```
Также он содержит найденную **дельту** и **stable sign** шаблона, если они были найдены.

***SO*** - Yandex.Mail спам оборона.

***MinHash*** - алгоритм для быстрого поиска похожих документов на основе [Jacquard Index](https://en.wikipedia.org/wiki/Jaccard_index). 
Более подробный рассказ можно найти [здесь](https://medium.com/engineering-brainly/locality-sensitive-hashing-explained-304eb39291e4)

***SimHash*** - алгоритм для поиска похожих документов на основе их контента, утверждается что документы имеющие схожие 
признаки имеют два sim hash'a который близки по [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance), 
более подробно можно прочитать [здесь](http://matpalm.com/resemblance/simhash/)
