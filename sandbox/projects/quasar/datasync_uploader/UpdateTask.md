Таска datasync_uploader позволяет использовать бинарные задачи. Для того, чтобы залить
новую задачу на прод, надо сделать:

```
# Run tests
ya make -tt sandbox/projects/quasar/datasync_uploader

# Compile binnary task. 
# !!! By now you can do it only on linux system. Binnary task built on MacOs will fail with strange message
ya make --checkout sandbox/projects/quasar/datasync_uploader/task

# Upload task binnary
./sandbox/projects/quasar/datasync_uploader/task/task upload --attr target=sandbox/projects/quasar/datasync_uploader --attr release=test

# !!! go to https://sandbox.yandex-team.ru/resources add attribute filter target=sandbox/projects/quasar/datasync_uploader and ensure that appropriete resource was created 

# Test it via sandbox GUI
# ...

# Send task code on review
# ...

# Release it via 
 ./sandbox/projects/quasar/datasync_uploader/task/task upload -attr target=sandbox/projects/quasar/datasync_uploader --attr release=stable

```