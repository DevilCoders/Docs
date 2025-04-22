# Yt http-proxy log analysis
Map-reduce based YT logs analysis via yt python api

### Scheme
1. Enrich proxy logs, write results to YT
2. Analyze enriched log, write results to YT by analysis type
3. Read results from YT and send them to Splunk via HEC
