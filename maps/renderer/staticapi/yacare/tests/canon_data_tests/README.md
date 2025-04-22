# API response visual tests

Tests use local files from `maps/renderer/staticapi/yacare/tests/data/tiles` as input tiles to render map image.

After adding new test:
1. Optionally remove content of data/tiles directory if it is needed to reload all tiles.
2. Call `ya m -A -Z --test-param LOAD_TILES=1` to load tiles from production that are used in tests and save them to data/tiles directory.
3. Commit changes in data/tiles and canon_data_tests directories.
