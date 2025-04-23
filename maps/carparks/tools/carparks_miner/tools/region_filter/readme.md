# The tool helps to filter ```filtered_points_id``` table by regions to reduce amount of data

## It can be used to prepare data for testing or for development purposes

## Usage

1. Get region ids you'd like to use in the filter from <https://geoadmin.yandex-team.ru/.> Run the tool:

    ```bash
    ./region_filter //home/maps/carparks/production/daps/mined/<DATE>/filtered_points_id <path_to_your_work_dir>/filtered_points_id [list_with_regions_id]
    ```

2. To update testing (if necessary) copy the output table to //home/maps/carparks/testing/daps/mined/<LATEST_DATE>/filtered_points_id to replace existing table
