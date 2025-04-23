Personal Travel Times
=====================

Implementation of the ideas proposed on the
[wiki page](https://wiki.yandex-team.ru/users/jagauthier/notes/PersonalisedTravelTimes).
Below is an example of a typical run of the scripts, that shows in which order
they will be usually used:

1. *./core/snap_jams.py*: Snaps jam data to the road graph
2. B *./core/signals.py*: Loads signals for the observed time frame
3. B *./core/travel_times.py*: Aggregates signals by track
4. B *./core/tracks_polylines.py*: Creates a polyline for each track
5. B *./core/tracks_polylines_scoeff.py*: (Without scoeff table) Adds a speed
coefficient of 1.0 to each track-polyline
    OR *./core/tracks_categories_scoeff.py*, if one wants to create an enhanced
user profile
6. B *./core/predictions/tracks_real_times.py*: Calculates the observed time on each
track using any received signals
    OR *./core/predictions/tracks_segments_real_times.py* for an enhanced user profile
7. B *./core/predictions/tracks_prediction_times.py*: Calculates the production trip
time for each of the considered tracks
    OR *./core/predictions/tracks_segments_prediction_times.py* for an enhanced user
profile
8. C *./userprofile/_/user_profile.py*: Creates personal user profiles
9. C *./userprofile/basic/user_profile_trim.py* or
*./userprofile/basic/user_profile_sdevcap* to filter out some user profiles.
10. T *./core/tracks_polylines_scoeff.py*: Adds the appropriate speed coefficient to
each track-polyline
    OR *./core/tracks_categories_scoeff.py*, for an enhanced user profile
11. T *./core/predictions/tracks_prediction_times.py*: Calculates the trip time
for each of the considered tracks based on speed coefficients
12. T *./core/predictions/tracks_times_comparison.py*: Compares real and
prediction times

For convenience, scripts marked by B can be launched through *./basic_setup.py*,
which performs the computation of the missing tables only. Similarly, scripts
marked by C and T can be accessed via *./create_personal_profile.py* and
*analyse_travel_times_prediction.py* respectively.

./create_histogram.py generates the charts from the paper and ./create_statistics.py
runs YT jobs to create statistics

In the scripts' comments, tables are represented using the "key x subkey x value"
notation.

Any questions to be addressed to Jean Andre Gauthier (@jagauthier) or Alexsander
Liubitsky (@innocent).