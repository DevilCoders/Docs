# calculate-permission-role

Блок для вычисления:
1. есть ли у текущего пользователя доступ к пункту "Доступы" в навигации (userHasPermissionToRoles)
2. есть ли у текущего пользователя доступ к странице редактирования прав `/edit/roles` (userHasPermissionToRoles)
3. является ли текущий (или фейковый) пользователь владельцем (userHasOwnerRole)
