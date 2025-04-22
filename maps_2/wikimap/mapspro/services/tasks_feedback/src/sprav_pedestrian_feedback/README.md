Utility to take sprav pedestrian feedback from table at YT
and publish it to NK.

There are 2 actions:

1) publish-feedback:
  Take data from '//home/sprav/assay/tasker/walkers/maps/feedback_export' YT-table
  and publish it to NK as feedback.

2) accept-entrances:
  Take data from '//home/sprav/assay/tasker/walkers/maps/entrances_export' YT-table
  and publish it to NK as commit or as feedback.

There are 2 modes:

1) Periodical:
  Each time it runs it checks time of feedback that has been already published,
  and selects only new feedback. It reads and updates time mark of already processed
  feedback. Time of feedback is time of its submition to sprav

  you run it without any arguments: ./wiki-sprav-pedestrian-feedback --action publish-feedback

2) By hand:
  No checks, no updates on metainfo about proccesed feedback.

  You run it once with specified time interval:
      ./wiki-sprav-pedestrian-feedback --action publish-feedback --lower-feedback-time 1511195392253 --upper-feedback-time 1511195392263

  Times are measured as Unix time in ms. Ask sprav guys why this is so.
