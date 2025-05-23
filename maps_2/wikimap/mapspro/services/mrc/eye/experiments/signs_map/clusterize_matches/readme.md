Решаем задачу проверки матчинга и кластеризации объектов.

Мы имеем:

1. набор фотографий идентифицируемых при помощи уникального feature_id

2. набор объектов на каждой фотографии, идентифицируемых при помощи object_id уникального внутри одной фотографии. Объекты типизированы.

Вручную или автоматически объекты на парах фотографиях склеиваются. В результате формируется файл вида:

```json
{
    "features_pairs": [
        {
            "feature_id_1": 1,
            "feature_id_2": 2,
            "matches": [
                {
                    "object_id_1": 8,
                    "object_id_2": 1
                },
                ...
            ]
        },
        ...
    ]
}
```

Представленная утилита формирует по списку пар набор кластеров. Кластер состоит из списка пар:

```
[(<feature_id_1, object_id_1>; <feature_id_2, object_id_2>), ...]
```

Поскольку "связываются" на паре фотографий изображения одного и того же физического объекта (например, дорожного знака), то каждый подобный кластер
и будет описывать один физический объект.

Утилита может использоваться для решения двух задач:

#### Проверка консистентности разметки пар (```--validate```)

Проверяются три типа ошибок:

1. В разметке дважды помечена связью одна и таже пара объектов на паре фотографий.

2. В результате работы в один кластер попали два объекта на одной фотографии (например, были связи *<A, 1> <-> <B, 1> <-> <C, 1> <-> <A, 2>*, в таком случае
и объект 1 и объект 2 на фотографии *A* должны попасть в один кластер, т.е. на фотографии один физический объект оказался в двух разных местах)

3. В одном кластере не все представления объектов связаны (например, есть связи *<A, 1> <-> <B, 1>* и *<B, 1> <-> <C, 1>*, но отсутствует связь *<A, 1> <-> <C, 1>*)

#### Формируется список кластеров/физических объектов (```--clusterize```)

Формируется список кластеров и сохраняется в файл формата:

```json
{
    "clusters": [
        {
            "cluster_id": 0,
            "objects" : [
                {"feature_id": 1, "object_id": 3},

                ...

                {"feature_id": 5, "object_id": 8}
            ]
        },

            ...

        {
            "cluster_id" : 100,
            "objects" : [
                {"feature_id": 222,"object_id": 0},

                ...

                {"feature_id": 333,"object_id": 7}
            ]
        }
    ]
}
```

При этом выполняется валидация разметки, и имеется возможность исправить ошибки типа 3 и добавить недостающие связи, а так же проигнорировать остальные типы ошибок и сформировать результат.

### Аргументы командной строки

#### Валидация

Для валидации надо запустить программу с параметром ```--validate``` и передать файл с матчингами через параметр ```--input-path```. В этом случае программа попытается сформировать кластеры
и выведет в консоль количество валидных кластеров и общее количество кластеров.

В качестве дополнительных параметров при валидации можно использовать следующие:

1. ```--add-absent-links``` - после кластеризации добавятся связи между объектами, находящимися в одном кластере, но не связанные во входном файле

2. ```--print-error``` - кроме количества "хороших" и общего количества кластеров, для каждого кластера будут напечатаны ошибки, которые в нём есть (двойная связь, два объекта на одной
фотографии, не все связи).

3. ```--print-error-ext``` - будет распечатана полная информация об ошибках (например, если есть "двойная связь" будут разпечатаны feature_id фотографий и object_id на них)

#### Выделение кластеров

Для сохранения кластеров надо запустить программу с параметром ```--clusterize``` и передать файл с матчингами через параметр ```--input-path```. В этом случае программа попытается сформировать
кластеры и сохранить их в файл переданный в параметре ```--output-path```. Перед сохранением запустится процедура валидации и если какие-то кластеры содержат ошибку - файл не будет сохранен

В качестве дополнительных параметров можно использовать следующие:

1. ```--add-absent-links``` - после кластеризации добавятся связи между объектами, находящимися в одном кластере, но не связанные во входном файле

2. ```--ignore-errors``` - результат кластеризации не валидируется и сохраняетс "как есть", т.е. с возможными ошибками

3. ```--objects-path``` - файл с объектами в формате:

```json
{
  'features_objects': [
    {
      'feature_id': 1
      'objects': [

      ]
    }
  ]
}
```

В случае если файл с объектами передан, то все объекты не упомянутые в файле с матчингами, превратятся в кластера из одного объекта. Если этот файл не передан, то кластера будут формироваться из
матчингов и содержать как минимум пару фотографий объекта.
