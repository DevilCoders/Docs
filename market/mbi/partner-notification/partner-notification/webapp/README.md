# Редактор шаблонов B2B уведомлений

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Обновление зависимостей node_modules для сборки фронта
```bash
$ rm -rf node_modules/ && yarn install && tar czf node_modules.tar.gz node_modules && ya upload --ttl=inf -T=JAVA_LIBRARY -d="Partner-Notifications node_modules cache" node_modules.tar.gz
```
Команда удалит старые зависимости, установит новые, поместит в архив и зааплоадит в sandbox.

После выполнения аплоада, в консоли появится ссылка на новый ресурс. ID нового ресурса необходимо прописать в файле [/build-tools/node_modules.ya.make](/arcadia/market/mbi/partner-notification/partner-notification/webapp/build-tools/node_modules.ya.make) вместо старого.
```bash
FROM_SANDBOX(FILE 3316617020 OUT_NOAUTO node_modules.tar.gz)
```

### Примеры команд для аплоада в sandbox всех зависимостей сборки
```bash
$ ya upload --ttl=inf -T=JAVA_LIBRARY -d="Node.js v16.14.0 (darwin, x64)" node.tar.gz

$ ya upload --ttl=inf -T=JAVA_LIBRARY -d="Node.js v16.14.0 (linux, x64)" node.tar.gz

$ ya upload --ttl=inf -T=JAVA_LIBRARY -d="yarn v1.22.17" yarn.tar.gz

4 ya upload --ttl=inf -T=JAVA_LIBRARY -d="Partner-Notifications node_modules cache" node_modules.tar.gz
```

NB: Версии Node.js для Linux и Macos отличаются. При обновлении необходимо собирать и аплоадить версии Node.js для обеих платформ.

ID обновленных ресурсов необходимо прописать в make-файлы в директории [/build-tools](/arcadia/market/mbi/partner-notification/partner-notification/webapp/build-tools).

## Available Scripts

In the project directory, you can run:

### `yarn start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `yarn test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `yarn build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `yarn eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
