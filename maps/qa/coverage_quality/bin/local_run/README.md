### What is that
Utility to calculate QA metrics such as *bugs in prod*, *minor bugs by testers*,  *minor bugs not by testers* and publish them to **StatFace**.

### How to run
Script uses several external services(YT, StatFace, ABC) so you need to authenticate yourself. The best case is when you authenticate as **robot-maps-qa**, because ACL in YT and StatFace are configured such that random person cannott write data there. Just provide tokens as environment variables like that:
`YT_TOKEN=* STATFACE_TOKEN=* ABC_TOKEN=* ./local_run (other options)`
