# @yandex-int/package-selector

Библиотека для листинга пакетов фронтенд-монореп.

## Использование

CLI:

```
npx @yandex-int/package-selector --root=path [options...]

List monorepo packages

Options:
  --version              Show version number                            [boolean]
  --help                 Show help                                      [boolean]
  --root                 root path                                       [string][default: .]
  --config               config path                                     [string]
  --names                include only packages with specified names       [array]
  --public-only          include only public packages                   [boolean]
  --changed              vcs: include only changed packages             [boolean]
  --since-commit         vcs: since commit to build diff,
                         defaults to merge-base with trunk               [string]
  --till-commit          vcs: till commit to build diff, defaults to ''  [string]
  --ignore-common-files  vcs: ignore changes not related to any package [boolean]
  --include-vcs-state    vcs: add package state to results,
                              but don't filter packages                 [boolean]
  --with-dependents      recursively include dependent packages         [boolean]
  --with-dependencies    recursively include dependencies               [boolean]
  --json                 output json                                    [boolean]
```

API:

```typescript
import { PackageSelector, Package, IPackageGraph } from "@yandex-int/package-selector";

const selector = new PackageSelector(process.cwd());

const packages: Array<Package> = await selector.getPackages();
const graph: Array<IPackageGraph> = await selector.getPackageGraph();

const changedPackages = await selector.select({ includeVcsState: true });
```
