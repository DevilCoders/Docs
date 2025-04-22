# How to update test data

## Collect queries

At the time of writing there are so called wizard squeezes kept on Hahn. Use them like this if available:

    USE hahn;
    SELECT
    search_props["norm"] AS query, region
    FROM RANGE(`//home/geo-search/wizards_squeeze/daily/wizards`, `2019-03-19`, `2019-03-20`)
    WHERE DictContains(search_props, "UPPER.Avia.FromSource") OR DictContains(search_props, "UPPER.Rasp.FromSource")
    AND query IS NOT NULL
    LIMIT 10000

Then: Full results -> Download as TSV

## Run begemot to get GeoAddrRoute results

    ./ya make -r web/daemons/begemot search/begemot/data/Wizard
    cat gar-10k.tsv | junk/grand/urlquote.py | web/daemons/begemot/begemot -d search/begemot/data/Wizard/search/wizard/data/wizard/ --test-cgi | ./ya tool jq -c ".[0].rules.GeoAddrRoute" > gar-10k.jsonl
    paste gar-10k.tsv gar-10k.jsonl | awk -F $'\t' '{if($3 != "null") {print;}}' > test_data/geoaddr-route-input.tsv
