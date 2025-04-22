# ymaps3-react

## Getting started

1. Install recommenden node via `nvm install`.
2. Install deps with `npm ci`.
3. Run `npm start`, address of the cases will be [http://localhost:8000/cases/](http://localhost:8000/cases/).

## Publish

For versioning [SemVer](https://semver.org/) is used.

1. (optional) If needed, implement changes in [@yandex-int/ymaps3](https://github.yandex-team.ru/maps/maps/tree/dev/ymaps3) and [publish](https://github.yandex-team.ru/maps/maps/blob/dev/ymaps3/CONTRIBUTING.md#publish-the-package) package.
2. Implement feature and push to the arcadia.
3. If you need to bump version, run `npm version patch` (or `minor`/`major`). Commit and push changes.
4. Create pr with `arc pr create`.
5. Pass the code review. If you do not know from who request a review see [abc jsapi 3.0](https://abc.yandex-team.ru/services/maps-front-jsapi-3/).
6. Test. To run storybook use `npm run storybook`.
7. Merge. CI will automatically publish package if needed.

See:

1. [Maps front repo docs](https://a.yandex-team.ru/arc/trunk/arcadia/maps/front/README.md).
2. [DevExp](https://github.yandex-team.ru/devexp/devexp) review ui.

## Testing

Use `npm run hermione` for testing. Then run `npm run hermione:gui` to view passed and failed tests.

## Add new or change icon

Add file to `icons` directory with name in `kebab-case`. File will be built to css class `.ymaps3x0-react--icon-<icon name>` automatically on commit.

Don't forget to add icon name to [MapIcon](./src/MapControls/MapIcon.tsx) `icon` prop type if it should be exported.

**Note**: The icons are stored in the `icon` directory in the namespaces folders (for example, the path to the `control` icons is `icons/contol/<control>.svg`). You should avoid storing icons at the top level of the `icon` folder.

Result `css` file will be automatically saved in `src/<some component>/icons.css` file. Don't forget to import this file in your React component index file.

**Note**: All files from directory `icons` and results `css` files will be automatically staged on commit.

**Note**: If you also want to add namespace or change some, you should make sure that the `namespace` and `component path` is added to [tools/build-css.ts](./tools/build-css.ts:40) new logic mapping.

## Documentation (руководство и справочник)

https://yandex.ru/dev/maps/jsapi/doc/3.0/dg/concepts/map.html

1. Open TeamCity https://teamcity.yandex-team.ru/buildConfiguration/DocContent_TechOutNewDeploy_Maps_JsApi?mode=branches
2. Click `Run` for `arcadia/trunk`
