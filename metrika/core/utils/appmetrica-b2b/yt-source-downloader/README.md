# yt-source-downloader



Usage: ./yt-source-downloader/yt-source-downloader [OPTIONS] [ARG]...

Required parameters:
  --yt-cluster VAL   ex: hahn
  --yt-token VAL     token for yt prod
  --yt-table VAL     path to table on with appmetrica events, like
  //home/metricmob/b2b_test_data/input_events
  --output-path VAL  path to save data

  Optional parameters:
{-V|--svnrevision} print svn version
{-?|--help}        print usage

Free args: min: 0, max: unlimited

Default usage example:
  YT_TOKEN=$(head ~/.yt/token); ./yt-source-downloader --yt-cluster=hahn  --yt-table=//home/metricmob/b2b_test_data/input_data_osval --yt-token=$YT_TOKEN --output-path=./data/
