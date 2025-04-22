# yt-source-uploader

Usage: ./yt-source-uploader [OPTIONS] [ARG]...

Required parameters:
  --yt-cluster VAL   ex: hahn
  --yt-token VAL     token for yt prod
  --yt-table VAL     path to table on with appmetrica events, like //home/metricmob/b2b_test_data/input_events
  --input-file VAL   path to file with protoseq events

  Optional parameters:
{-V|--svnrevision} print svn version
{-?|--help}        print usage

Free args: min: 0, max: unlimited

Default usage example:
 YT_TOKEN=$(head ~/.yt/token); ./yt-source-uploader --yt-cluster=hahn --yt-table=//home/metricmob/b2b_test_data/input_data_$USER --yt-token=$YT_TOKEN --input-file=input_data
