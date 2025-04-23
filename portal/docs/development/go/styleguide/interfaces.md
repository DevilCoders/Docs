## Accepted Interfaces

Мы применяем подход, который называем **accepted interfaces**.
Это означает, что если какой-либо модуль (структура, метод) зависит от другого модуля, то нужно делать зависимость от интерфейса, а не от реализации. При этом интерфейс нужно определять приватным в том месте, где он используется.

Противоположный подход - использовать публичные интерфейсы. Такой подход тоже используется ([пример](https://a.yandex-team.ru/arc_vcs/portal/avocado/morda-go/pkg/contexts/base.go?rev=r9651790)), но предпочтение стоит отдавать
приватным интерфейсам.

Подход с accepted interfaces дает преимущества:
- если у реализации много методов, определение приватного интерфейса в месте использования позволяет
определять в интерфейсе только те методы, которые именно здесь нужны.
- приватные интерфейсы проще мокать, а значит код легче тестировать.
- сокращается число зависимостей между пакетами - нет необходимости импортировать пакет с реализацией или публичным интерфейсом.
- легче начать использовать другую реализацию.

Мы кладем такие приватные интерфейсы в отдельный файл interfaces.go.
Пример пакета, в котором используются приватные интерфейсы: [mordacontent](https://a.yandex-team.ru/arc_vcs/portal/avocado/libs/utils/mordacontent/interfaces.go?rev=r9652181)

{% cut "Пример" %}

Представим, что есть тип, описывающий человека по имени Иван. Иван по профессии пилот, а еще у него есть сын-первоклассник.

Иван верит в развитие технологий, и поэтому попросил своего друга из Яндекса перенести его сознание в компьютер.

ivan.go
```
    package ivan

    import time

    type Ivan struct{
        age 	int
        married bool
    }

    func (i Ivan) NewIvan() Ivan {...}

    func (i Ivan) TakeOff() error {...}

    func (i Ivan) LandOn() error {...}

    func (i Ivan) PlayFootball(duration time.Duration) {...}

    func (i Ivan) CheckDiary() int {...}

    func (i Ivan) GoToParentMeeteng() error {...}
```

Его сын тоже захотел перенести сознание в компьютер, но ему по-прежнему нужен родитель, чтобы ходить на родительские собрания, проверять дневник и играть в футбол по выходным.

son.go
```
    package son

    import time

    type parent interface {
        func PlayFootball(duration time.Duration)
        func CheckDiary() int
        func GoToParentMeeteng() error
    }

    type Son struct{
        parent parent
    }

    type NewSon(parent parent) Son {
        return Son{father: father}
    }

    func (s Son) PlayFootball(duration time.Duration) error {
        s.parent.PlayFootball(duration)
        ...
    }

    func (s Son) GoToSchool() error {
        ...
        mark := s.parent.CheckDiary()
        err := s.parent.GoToParentMeeteng()
        if mark >= 4 && err == nil {
            err = s.PlayFootball(time.Hour)
        }
        ...
    }
```

На работе тоже оказались готовы к тому, что вместо Ивана будет работать его цифровая копия.

plane.go
```
    package plane

    type pilot interface {
        TakeOff() error
        LandOn() error
    }

    type Plane struct {
        pilot pilot
    }

    func NewPlane(pilot pilot) Plane {
        return Plane{pilot: pilot}
    }

    func (p Plane) Fly(destination string) error {
        ...
        err := p.Pilot.TakeOff()
        if err != nil {
            return err
        }
        ...
        err = p.Pilot.LandOn()
        if err != nil {
            return err
        }
        ...
    }
```

Как видно из примера, в каждом пакете, который зависит от Ивана, зависимость не от структуры Ivan, а от интерфейса, который им реализуется. При этом в каждом из двух зависящих пакетов интерфейсы объявлены локальными и приватными.

Таким образом появляется возможность более гибко подменять реализацию. Скажем, у типа Son в поле parent вместо Ивана может быть его жена,
которая тоже умеет ходить на родительские собрания и проверять дневник (и играть в футбол ¯\_(ツ)_/¯).

В самолете тоже могут поменять Ивана на другого пилота, если Иван заболеет, даже если у заменяющего нет детей и не реализованы методы проверки дневника и тд.

Кроме того, цифрового Ивана можно заменить тестовыми копиями, чтобы протестировать реализации сына и самолета. При этом в тестовых копиях не придется реализовывать ненужные методы.

При альтернативном подходе - если бы пакеты зависели от публичного интерфейса Ivan со всеми его методами - его бы не получилось так легко заменить.

{% endcut %}
