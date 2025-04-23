# B2Bgeo asyncsolver logs parser

[[toc]]

## General information

This tool is designed to extract preparation and execution time from asyncsolver's logs.
Logs are grouped by task size(e.g. tiny, huge), and then are grouped by logged operation name. For such each group minimum, maximum, mean, median, sum, 90 percentile and 99 percentile are calculated.

## Input parameters

| Name | Description | Is the parameter required |
| ---- | ----------- | ------------------------- |
| `--source-path` | Path to the file with asyncsolver's logs in format TSKV | Yes |
| `--destination-path` | Path to the file with output data. The resulting dataframe will be written to this file. | Yes |
| `--operations-with-hierarchy` | Whether it is necessary to display the full names of operations include the hierarchy of calls | No |
| `--hierarchy-path` | File path with calls hierarchy. File format. Calling_function_operation_name Called_function_operation_name (both names must not contain spaces). If the function does not have a calling function, you should leave the Calling_function_operation_name empty. | No |

You can use [the following yql-request](https://yql.yandex-team.ru/Operations/YQfpQguEIy7t1a36YUJy3FOoz5CQJ6STohIUywrZCUs=) to get a file with logs.

## Output

The results of the tool's work are a dataframe at `destination_path` file and a group of tables.
Separate table is generated for each task size. Each table has characteristics described above for each logged operation.

Dataframe has the following form:

| Task size | Operation name | Probes | Percentile90 | Percentile99 | Mean | Median | Min | Max | Sum |
| --------- | -------------- | ------ | ------------ | ------------ | ---- | ------ | --- | --- | --- |

## Usage

The tool outputs a data frame. It can be used as a dataset to view given operations timings.
You can use following tools to further analyze this data:
* [datalens](https://datalens.yandex-team.ru/wvh2r7c4eadup-dashbord-2021-07-27-28)
* jupyter (see /example/charts_example.ipynb)
* [sunburst diagram](https://st.yandex-team.ru/BBGEO-10225/attachments/36481196?) using the [script](https://github.com/matrohin/pie-analyzer)

