Utility to generate oneway hypotheses in terms of revision,
returning them in text format for MPRO import


Call example:

./hyp_export --revision-config services.development.xml --graph-version 18.01.31 --last-signals-day 2018-01-31
    --bbox-geo 41.614852,44.623703,41.865819,45.068649 --alarm-match-ratio 0.95 --min-both-edge-tracks 50 --max-funclass 7

Result example:

lon	lat	description	object_id
44.76115	41.711396	direction should be from-b-to-a	1504359816
44.808312	41.690169	direction should be from-b-to-a	1504363113
44.799854	41.69191	direction should be from-b-to-a	1504359315
44.815452	41.694139	direction should be from-b-to-a	1504361857
