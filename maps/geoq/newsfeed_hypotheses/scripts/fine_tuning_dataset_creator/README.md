### Binary for making dataset to fine tune newsfeed hypotheses classifier

#### Parameters

- `--start-date` - minimum date for hypotheses, format YYYY-MM-DD, default 2020-04-15
- `--feedback-table` - table with nmaps feedback, [default](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/feedback/db/feedback_latest)
- `--hypotheses-table` - table newsfeed hypotheses, [default](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/geoq-hypotheses/newsfeed/hypotheses)
- `--output-table` output table

#### Usage example

`./newsfeed_fine_tuning_dataset --output-table //home/maps/users/arbel0s/newsfeed/fine_tuning/dataset`
