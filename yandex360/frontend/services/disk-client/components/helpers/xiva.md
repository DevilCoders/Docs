Пуши про общие папки

1. Новое приглашение - invite_new:

   - для владельца

   {"root":{"tag":"share","parameters":{"type":"invite_new","for":"owner"}},"values":[{"tag":"user","parameters":{"first_invitation":1,"universe_login":"yanatest2@yandex.ru","universe_service":"email"},"value":""},{"tag":"folder","parameters":{"path":"/disk/images/pics/","gid":"6149240dd583681391853117dff86b4d","name":"pics","rights":660},"value":""}]}

   operаtion inviteFolder

   - для приглашенного

   {"root":{"tag":"share","parameters":{"type":"invite_new","for":"actor"}},"values":[{"tag":"owner","parameters":{"uid":"3000408567","name":"yana test"},"value":""},{"tag":"folder","parameters":{"hash":"67fda3a6d9a271e0923d1a1bceacd9cb","name":"dir2","rights":660},"value":""}]}

   model invitesFolder

2. Закрытие доступа

  - для владельца  - folder_unshared

  {"root":{"tag":"share","parameters":{"type":"folder_unshared","for":"owner"}},"values":[{"tag":"folder","parameters":{"path":"/disk/shared_folders/myfolder9/","gid":"9881d39eed62743fb990efda1d3bf938","name":"myfolder9"},"value":""}]}

   operation unshare

  - для приглашенного, который еще не принял приглашение - invite_removed

  {"root":{"tag":"share","parameters":{"type":"invite_removed","for":"actor"}},"values":[{"tag":"folder","parameters":{"path":"/disk/myfolder7/","gid":"f81275590f52c7a2ec1dd2370bae9b25","name":"myfolder7"},"value":""}]}

  model invitesFolder

  - для пользователя - folder_unshared - такое же при удалении папки владельцем

  {"root":{"tag":"share","parameters":{"type":"folder_unshared","for":"user"}},"values":[{"tag":"folder","parameters":{"path":"/disk/dir2/","gid":"24263ca448b2665fc634846a6619a8c1","name":"dir2"},"value":""}]}

  удаление папки

  обновление space

  notification про то, что закрыт доступ

3. Отклонили приглашение

  - для владельца  - invite_rejected

  {"root":{"tag":"share","parameters":{"type":"invite_rejected","for":"owner"}},"values":[{"tag":"folder","parameters":{"path":"/disk/shared_folders/myfolder1/","gid":"0078710b9a2c4e3c9431e1f1d6215cf7","name":"myfolder1"},"value":""},{"tag":"user","parameters":{"uid":"140013252","name":"Vasily Pupkin"},"value":""}]}

   model usersFolder

   notification - ваше приглашение отклонили

  - для приглашенного

  {"root":{"tag":"share","parameters":{"type":"invite_rejected","for":"actor"}},"values":[{"tag":"folder","parameters":{"gid":"17baad20dd60c4d9f5d08e3a23e04d97","hash":"e8ca8f34a7145288add9e90ecc51716e","name":"dir1"},"value":""}]}

  operation rejectInvite

4. Принятие приглашения

 - для владельца

  {"root":{"tag":"share","parameters":{"type":"invite_approved","for":"owner"}},"values":[{"tag":"folder","parameters":{"path":"/disk/shared_folders/myfolder2/","gid":"16c9b60cfe1a54b9d30a70ef9ee0fe80","name":"myfolder2"},"value":""},{"tag":"user","parameters":{"uid":"140013252","name":"Vasily Pupkin"},"value":""}]}

  model usersFolder

  нотификация  - приняли ваше приглашение

  - для того, кто принял

  {"root":{"tag":"share","parameters":{"new":1392385927861927,"old":"1392385927793848","for":"actor","type":"invite_approved"}},"values":[{"tag":"folder","parameters":{"path":"/disk/dir2/","gid":"1c5bcffff1ecdf31d810612bff1179ef"},"value":""}]}

  operation activateInvite

  - для другого пользователя папки

  {"root":{"tag":"share","parameters":{"type":"invite_approved","for":"user"}},"values":[{"tag":"folder","parameters":{"path":"/disk/dir2/","gid":"1c5bcffff1ecdf31d810612bff1179ef","name":"dir2"},"value":""},{"tag":"user","parameters":{"uid":"3000408568","name":"yana test"},"value":""}]}

  model usersFolder

  нотификация - кто-то еще теперь тоже пользуется папкой, к которой у вас есть доступ

5. Удаление папки пользвателем

  - для владельца

  {"root":{"tag":"share","parameters":{"type":"user_has_left","for":"owner"}},"values":[{"tag":"folder","parameters":{"path":"/disk/shared_folders/myfolder2/","gid":"16c9b60cfe1a54b9d30a70ef9ee0fe80","name":"myfolder2"},"value":""},{"tag":"user","parameters":{"uid":"140013252","name":"Vasily Pupkin"},"value":""}]}

  model usersFolder

  notification - пользователей папки стало меньше

  - для удалившего общую папку

  {"root":{"tag":"share","parameters":{"type":"user_has_left","for":"actor"}},"values":[{"tag":"folder","parameters":{"path":"/disk/dir2/","gid":"1c5bcffff1ecdf31d810612bff1179ef"},"value":""}]}

  operation delete (не в корзину, без нотификации)

  - для другого пользователя этой папки

  {"root":{"tag":"share","parameters":{"type":"user_has_left","for":"user"}},"values":[{"tag":"folder","parameters":{"path":"/disk/dir2/","gid":"1c5bcffff1ecdf31d810612bff1179ef","name":"dir2"},"value":""},{"tag":"user","parameters":{"uid":"3000408221","name":"yana test"},"value":""}]}"

  model usersFolder


6. Смена прав

  - для владельца

  {"root":{"tag":"share","parameters":{"type":"rights_changed","for":"owner"}},"values":[{"tag":"folder","parameters":{"path":"/disk/shared_folders/myfolder3/","gid":"341cfccda2bb37e3ce6c2d37d06e14f7","name":"myfolder3","rights":640},"value":""}]}

  operation accessFolder

  - для пользователя

  {"root":{"tag":"share","parameters":{"type":"rights_changed","for":"actor"}},"values":[{"tag":"folder","parameters":{"path":"/disk/myfolder2/","gid":"1712b3a37530bdb5dbe872d34f3c2e32","name":"myfolder2","rights":640},"value":""}]}"

  обновить ресурс, проверить - обновится ли кнопки тулсета

  нотификация - вам поменяли права на папку ??

  - для другого пользователя

  {"root":{"tag":"share","parameters":{"type":"rights_changed","for":"user"}},"values":[{"tag":"folder","parameters":{"path":"/disk/myfolder2/","gid":"1712b3a37530bdb5dbe872d34f3c2e32","name":"myfolder2","rights":640},"value":""},{"tag":"user","parameters":{"uid":"3000408567","name":"yana test"},"value":""}]}"

  нужно ли вообще обрабатывать? (нигде не видно прав других пользователей)
  ???
  нотификация - у кого-то изменились права на папку, к которой у вас есть доступ ???

7. Удаление из папки

  - для владельца
  удаление того, кто принял
  {"root":{"tag":"share","parameters":{"type":"user_was_banned","for":"owner"}},"values":[{"tag":"folder","parameters":{"path":"/disk/shared_folders/myfolder2/","gid":"1712b3a37530bdb5dbe872d34f3c2e32","name":"myfolder2"},"value":""},{"tag":"user","parameters":{"uid":"3000408568","name":"yana test"},"value":""}]}
  удаление того, кто не принял
  {"root":{"tag":"share","parameters":{"type":"invite_removed","for":"owner"}},"values":[{"tag":"folder","parameters":{"path":"/disk/shared_folders/myfolder3/","gid":"341cfccda2bb37e3ce6c2d37d06e14f7","name":"myfolder3"},"value":""},{"tag":"user","parameters":{"universe_login":"yanatest2@yandex.ru","universe_service":"email","name":"","avatar":""},"value":""}]}

  нужно обновить usersFolder

  - для пользователя еще не принявшего приглашение

  {"root":{"tag":"share","parameters":{"type":"invite_removed","for":"actor"}},"values":[{"tag":"folder","parameters":{"path":"/disk/myfolder3/","gid":"341cfccda2bb37e3ce6c2d37d06e14f7","name":"myfolder3"},"value":""}]}"

  model invitesFolder

  - для пользователя, который уже принял приглашение

  {"root":{"tag":"share","parameters":{"type":"user_was_banned","for":"actor"}},"values":[{"tag":"folder","parameters":{"path":"/disk/myfolder2/","gid":"1712b3a37530bdb5dbe872d34f3c2e32"},"value":""}]}"

  удалить папку

  обновить всех родителей

  нотификация - вас лишили доступа

  обновить space

  - для другого пользователя, который тоже пользуется папкой

  {"root":{"tag":"share","parameters":{"type":"user_was_banned","for":"user"}},"values":[{"tag":"folder","parameters":{"path":"/disk/myfolder5/","gid":"a7f6828d2a926607cc7285f3157fa94b","name":"myfolder5"},"value":""},{"tag":"user","parameters":{"uid":"3000408568","name":"yana test"},"value":""}]}"

  обновить usersFolder