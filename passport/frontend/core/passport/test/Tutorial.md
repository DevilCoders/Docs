# Как начать писать тесты и завести друзей

## Структура тестов

[Mocha](http://visionmedia.github.io/mocha/) —
Фреймворк для написания тестов. Мы используем BDD-suite:

```Javascript
describe('Some module', function() {
  it('должен работать', function() {
    // Любой код, который при выполнении не кидает эксцепшен считается прошедшим тестом.
  });
});
```

## Проверки

[Expect.js](https://github.com/LearnBoost/expect.js/) — набор проверок, сравнений и ожиданий, которые тест должен пройти:

```Javascript
describe('Expect.js', function() {
  it('должен кидать ошибку, когда видит несоответствие реальности ожиданиям', function() {
    expect(true).to.be(false); // Test fails
  });

  it('должен уметь делать разные проверки', function() {
    expect({a: 'bc'}).to.eql({a: 'bc'});
    expect(function() { throw new Error('Hey! An error!'); }).to.throwException('Hey! An error!');
  });
});

```

## Независимость от внешнего мира

Мы пишем юнит-тесты, это значит, что в одном тесте мы тестируем только одну функцию.
[Sinon.js](http://sinonjs.org/docs/) подделывает объекты, функции, запросы и время, чтобы мы не зависели от окружения:

```Javascript
describe('Sinon.js', function() {
  it('должен уметь шпионить за вызовами функций', function() {
    sinon.spy($, 'ajax');
    $.ajax('a parameter');
    expect($.ajax.calledWithExactly('a parameter')).to.be.ok();

    // Восстанавливаем настоящий ajax
    $.ajax.restore();
  });

  it('должен уметь подделывать методы объектов, чтобы можно было получить контролируемое поведение', function() {
    var myObject = {
      method: function() {
        return this.otherMethod();
      },

      otherMethod: function() {
        return {some: 'thing'};
      }
    };

    sinon.stub(myObject, 'otherMethod').returns({other: 'thingie'});

    expect(myObject.method()).to.eql({other: 'thingie'});
    myObject.otherMethod.restore();
  });
});
```
