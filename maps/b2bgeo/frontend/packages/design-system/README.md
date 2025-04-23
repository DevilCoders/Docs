#B2B GEO design system

[Figma](https://www.figma.com/file/2xqM6FnZwjdOEaOrEx5QMj/Routing-Design-System)

## Contributing

### Development
Run Storybook for development - `npm run storybook`. The app will be avalaible on `http://localhost:6006`.

For each new component don`t forget to: 
* write a story with examples
* write a test if needed
* export component from common [index.ts](https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/frontend/packages/design-system/src/index.ts?rev=6e3d8505fc218ce5e0af6fe36725797c0f575b2d#L1) file

### Build and using components
After the job is done, run `npm run bootstrap` in a root folder to build a new component and type definitions. 

Restart your working project after the `design-system` is bootstrapped. 

Use component in your project: 
```
import { GreatNewComponent } from '@b2bgeo/design-system/dist/components/GreatNewComponent'
```
