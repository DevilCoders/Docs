# Directory structure

- `layouts/` - layouts in `module.json` format with html file by side
    - `layouts/*.css/` - "css layouts", same as normal layouts, but without html file (i.e. module with dependencies, but without content).

- `src/bem/` - originally directory with BEM blocks. Name is preserved for easier transition.
    - `src/bem/blocks/` - blocks, each `.css` and `.styl` will produce a module named as file.

- `src/bevis/` - originally directory with BEViS blocks. Name is preserved for easier transition.
    - `src/bevis/blocks/{common,core,project}/` - blocks, each `.css` and `.styl` will produce a module names as file with `islets-` prefix. All classes inside will be prefixed with `islets_`.

- `src/common/` - common `styl` files for `src/bem/`, `src/bevis/`, and `../src/**/*.styl`.
