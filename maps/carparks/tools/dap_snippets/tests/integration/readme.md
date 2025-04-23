Test data consists of 3 organizations (100, 200, 300) and 3 toponyms
('А', 'Б' и 'В'). Below are examples of the naming convention being used.

Mined organization:
    id/target: 100 (200, 300 and so on)
    target lon, lat: 1.0 0.1
    cluster point 1: 1.0001 0.1
    cluster point 2: 1.0002 0.1
    ...
    cluster point X: 1.000X 0.1

Mined toponym:
    id: 11 (12, 13 and so on)
    target and target lon, lat: 11.0 0.11
    cluster point 1: 11.0001 0.11
    cluster point 2: 11.0002 0.11
    ...
    cluster point X: 11.000X 0.11

Sprav organization or toponym:
    Cluster point X for target (lon, lat) Z.0 0.Z: Z.00X0 0.Z

Nyak toponym:
    Cluster point X for target (lon, lat) Z.0 0.Z: Z.0X00 0.Z

[Picture](https://wiki.yandex-team.ru/users/retinskii/dapsnippetsintegrationtest/)
