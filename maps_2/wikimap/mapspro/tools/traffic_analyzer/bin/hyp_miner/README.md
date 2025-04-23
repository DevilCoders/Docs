Utility to generate oneway hypotheses in terms of road graph.


Call example:

./hyp_miner --graph-version 18.01.31 --last-signals-day 2018.01.31 --bbox-geo 56.278902,43.846226,56.372373,44.198476 
--alarm-match-ratio 0.92 --min-both-edge-tracks 30 --max-funclass 7 --average-window 1

Result example:

{"roadId":34651691,"roadTraffic":{"bothEdgeTracks":130,"matchRatio":0.9230769230769231,
    "graphVersion":"18.01.31","dayBegin":"2018-01-31","dayEnd":"2018-02-01"}}
{"roadId":59642528,"roadTraffic":{"bothEdgeTracks":222,"matchRatio":0.9864864864864865,
    "graphVersion":"18.01.31","dayBegin":"2018-01-31","dayEnd":"2018-02-01"}}
