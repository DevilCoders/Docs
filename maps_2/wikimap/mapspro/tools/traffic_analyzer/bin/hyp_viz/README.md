Utility to vizualize geometry of roads of oneway hypotheses - both graph and revision.
The result is polylines in format suitable for Easyview utility.


Call example:

hyps_graph.txt:

{"roadId":34651691,"roadTraffic":{"bothEdgeTracks":130,"matchRatio":0.9230769230769231,
    "graphVersion":"18.01.31","dayBegin":"2018-01-31","dayEnd":"2018-02-01"}}
{"roadId":59642528,"roadTraffic":{"bothEdgeTracks":222,"matchRatio":0.9864864864864865,
    "graphVersion":"18.01.31","dayBegin":"2018-01-31","dayEnd":"2018-02-01"}}

hyps_rev.txt:

{"positionMerc":{"x":4896509.829802278,"y":7581728.131918165},"revId":{"objectId":5128642,"commitId":41846424},"direction":"from-a-to-b",
    "roadTraffic":{"bothEdgeTracks":130,"matchRatio":0.9230769230769231,
        "graphVersion":"18.01.31","dayBegin":"2018-01-31","dayEnd":"2018-02-01"}}
{"positionMerc":{"x":4894188.674387352,"y":7589146.879459806},"revId":{"objectId":2124635680,"commitId":73069001},"direction":"from-a-to-b",
    "roadTraffic":{"bothEdgeTracks":222,"matchRatio":0.9864864864864865,
        "graphVersion":"18.01.31","dayBegin":"2018-01-31","dayEnd":"2018-02-01"}}


./hyp_viz --hyps-graph-file hyps_graph.txt --graph-version 18.01.31
    --hyps-revision-file hyps_rev.txt --revision-config conf.dev.xml | easyview

hyp_viz stdout:

!linestyle=red:8
43.942391 56.300624 43.942359 56.300576
43.980928 56.288615 43.980819 56.288583
!linestyle=blue:4
43.942552 56.300861 43.942391 56.300624
43.981249 56.288709 43.980928 56.288615
