# Редактор behavior trees для Pod Agent
Это форк репозитория https://github.com/behavior3/behavior3editor.git

## Как развернуть behavior3editor локально:
1. curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
2. sudo apt-get install -y nodejs
3. sudo npm install -g bower
4. sudo bower install --allow-root
5. sudo chown -R username:username ~/.config # вместо username ваш юзер
6. sudo chown -R username:username ~/.npm # вместо username ваш юзер
7. npm install # нужно делать в корневой папке с едитором
8. sudo npm install --global gulp-cli # нужно делать в корневой папке с едитором
9. gulp serve # нужно делать в корневой папке с едитором
10. http://127.0.0.1:8000 # have fun
