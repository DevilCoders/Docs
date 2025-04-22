Utility to generate oneway hypotheses in terms of revision and publish them to NK.


####################################################
### Process entire world. This call can be placed
### in cron to generate hypotheses each day
####################################################

./wiki-oneway-hyps-generator --max-hyps 200 --average-window 7
--alarm-match-ratio 0.92 --min-both-edge-tracks 30 --max-funclass 7

It means that maximum 200 hypotheses will be generated for the whole world
with averaging for the last seven days, starting from the day before yesterday.
The graph version that will be used is the last matched at
hahn://home/maps/jams/production/data/travel_times

###############################################
### Generate all hypotheses fo Turkey Bursa
###############################################

./wiki-oneway-hyps-generator --graph-version 18.03.06-1 --last-signals-day 2018.03.18 --average-window 7
--bbox-geo 40.057249,28.647431,40.418237,29.397248 --alarm-match-ratio 0.92 --min-both-edge-tracks 20 --max-funclass 7
