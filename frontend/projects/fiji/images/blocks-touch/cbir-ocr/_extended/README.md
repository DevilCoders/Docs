cbir-ocr_extended
============

Попадает ли элемент в выделенную область
## _isBlockInSelection(block, x1, y1, x2, y2)

На вход передается блок и координаты начала и конца жеста

1) Находим координаты углов повернутого блока
    При вызове getBoundingClientRect получаем координаты повернутого блока, вписанного в прямоугольник.
    Зная размеры и угол поворота вычисляем координаты углов:
    ![](https://jing.yandex-team.ru/files/ahryapov/Find%20the%20rectangle%20inscribed%20in%20another%20%20rectangle%281%29.png)

2) Определяем пересекаются ли отрезки (границы блока и жест):
    http://gospodaretsva.com/urok-32-peresekayutsya-li-dva-otrezka.html
