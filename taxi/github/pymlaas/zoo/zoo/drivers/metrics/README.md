# Driver Metrics

Hi!

This code creates a nile flow, which contains windowed metrics
(e.g. how many orders there where in a city a week before date).
Generally you just provide a table with ids + dates and a list of metrics and get the required metrics back
You can use them either as features or as targets in you model. You can also use table bindings from tables.py


## Usage

### To Start

First of all you should specify the dates interval (both are included, as in Nile range) of your data and optionally the path for the metrics to store.

```python
from zoo.drivers.metrics.calculate_metrics import configure_job

dates = (start_date, end_date) # datetime.Date or datetime.datetime objects

configure_job(job, dates, path='//foo/bar')
```

Then you just provide a list of objects for which you want to calculate metrics, provide a list of metric names
(for now you can lookup the metrics in the metrics config folder),
specify the main id (could be a tuple) and provide the name of the date field (optional with a default)

```python
from zoo.drivers.metrics.calculate_metrics import calculate_metrics

metrics = calculate_metrics(source_table, "city", ["n_orders_7"], "date")
```

If you prefer a more OOP style:

```python
metrics = source_table.call(calculate_metrics, "city", ["n_orders_7"], "date")
```

### If you need source tables which are used for metrics

You can also use the source tables seperately from the main purpose of this project 

```python
from zoo.drivers.metrics.tables import orders

orders_stream = orders(job) # take all orders for the dates specified in the add_dates_to_job
```

Take custom dates:

```python
orders_stream = orders(job, (start_date, end_date))
```

### Caching

The metrics support caching! It doesn't work 100% good now, but still,
if you do not want to recalculate metrics and get them from cache, just run the job with appropriate checkpoints (they will not conflict with your custom checkpoints)

```python
job.run(checkpoints=("metrics_city",))
```

This checks if you changed the dates in `configure_job`. For now it won't work correctly, if you change the list of drivers. It will alsi fail to execute if you extended the metrics list

## Architecture
To be written


## TODO

1. Upgrade the caching:
    1. Cache metrics partially
    2. Do not recalculate some metrics if they are already calculated
    2. Check if metrics are already calculated for some objects
    3. Cache dates partially
    4. what to do with columns, contained in experiment? DONE
    5. Learn to get all of the metrics unrelated
3. API improvals:
    1. Infer the intermediate metrics so that the user can omit them
    1. restructure metrics_config and allow `calculate_metrics` to take objects instead of metric_names
    2. Allow to pass custom metrics without changing the main code
    3. Merge tables and table_writers modules
4. Peformance
    1. Think of windowed calculation instead of map-side join
    2. Cache partial sums
5. COSMO
    1. Find out how to make window functions smart
