# Change KPI experiment

change_kpi_experiment.py - Reads whitelist dumped by Driver Offer, computes
new kpi and new kpi bonus for every unique_driver_id for every custom experiment group,
splits to top and bottom by ranking score, splits bottom to control, default 
and custom groups, then joins top, default and custom groups into new whitelist.

calc_kpi_bonus_functions.py - functions for calculating "score" (one of possible ranking 
scores), mean cost by city and bonus sum. Written mostly by Gosha for Driver Offer 
and translated to py3.

split_functions.py - functions for random split.

## parameters

exp_date - start date of experiment (not today)

quantiles - quantile of the weekly success orders counts for the last 5 weeks. 
Used for min kpi cutoff as a precaution. Should be empty string if param
percents is chosen and vice versa.

percents - percent of the median of the weekly success orders counts for the 
last 5 weeks to add to the median. Used for min kpi cutoff as a precaution.

features_lag - days from experiment date to the date (=name) of the last existing 
prod features table.

metrics_lag - same for metrics table

kpi_plus_percents - percents that specifies custom groups of experiment. In each
group kpi = default kpi + percent / 100  * default kpi

max_kpi - max kpi for clipping bigger values

days_long - duration of experiment

money_multiplier

tariff_zone_blacklist - zones to put to top (=do not change)

bottom_percent - bottom percent to use in experiment


# Analytics 

analytics_nile.py - Joins all needed information for analytics then divides it
by experiment groups and then drops those groups to specified paths.

analytics_plot.py - Reads groups dropped by analytics_nile.py and draws various 
plots

## parameters

salt

exp_path - path for groups and checkpoint tables

whitelist - path of original whitelist

new_whitelist - path for new whitelist

config_name - name of config in configs directory

experiment_id - name of experiment in all_experiments table (or shorter one if 
use_id_as_fake == True)

use_id_as_fake - if param is True then all experiment_id's in all_experiments table would 
be cut by len(our experiment_id)

start_date - experiment start date for metrics and prod features

sessions_orders_table_path - product of collect_data from pymlaas

duration - duration of experiment in days (other durations than 7 are useless for now)

test_groups_of_interest - only test groups of interest from config (uses all by default)

yt_path - path for dumping groups and stats

local_dir - local directory for plots

score_type - score to use for ranking (experiment_score, ranking_target_n_orders_7, ranking_paid)

n_buckets - num of score groups
