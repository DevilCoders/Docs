### Разобрать waiting
Нужно актуализировать очередь релизов на выкладку (в чеклисте это называется "разобрать waiting").
Робот не разрешит выкладывать новый релиз, если он не находится в стадии **waiting-1** или **stable**.

Нам могут понадобится две команды (`overview` и `next-waiting`):
