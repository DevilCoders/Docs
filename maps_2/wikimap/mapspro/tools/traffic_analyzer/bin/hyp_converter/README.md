Utility to convert oneway hypotheses in terms of road graph to hypotheses in terms of revision.


Call example:

hyps_graph.txt:

{"roadId":34651691,"roadTraffic":{"bothEdgeTracks":130,"matchRatio":0.9230769230769231,
    "graphVersion":"18.01.31","dayBegin":"2018-01-31","dayEnd":"2018-02-01"}}
{"roadId":59642528,"roadTraffic":{"bothEdgeTracks":222,"matchRatio":0.9864864864864865,
    "graphVersion":"18.01.31","dayBegin":"2018-01-31","dayEnd":"2018-02-01"}}

./hyp_converter --revision-config conf.dev.xml --graph-version 18.01.31 < hyps_graph.txt

stdout:

{"positionMerc":{"x":4896509.829802278,"y":7581728.131918165},"revId":{"objectId":5128642,"commitId":41846424},"direction":"from-a-to-b",
    "roadTraffic":{"bothEdgeTracks":130,"matchRatio":0.9230769230769231,
        "graphVersion":"18.01.31","dayBegin":"2018-01-31","dayEnd":"2018-02-01"}}
{"positionMerc":{"x":4894188.674387352,"y":7589146.879459806},"revId":{"objectId":2124635680,"commitId":73069001},"direction":"from-a-to-b",
    "roadTraffic":{"bothEdgeTracks":222,"matchRatio":0.9864864864864865,
        "graphVersion":"18.01.31","dayBegin":"2018-01-31","dayEnd":"2018-02-01"}}
