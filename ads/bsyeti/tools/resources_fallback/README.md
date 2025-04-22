```
usage: resources_fallback [-h] [-c CONTOUR] [-a AGO] [-m MESSAGE] [-t TICKET]
                          [-r] [-s {sandbox,validator}] [-q] [--readme]

Fallback resources in case of any problems.

optional arguments:
  -h, --help            show this help message and exit
  -c CONTOUR, --contour CONTOUR
                        Contour ids. May be several. May use 'eagles' or
                        'buzzards' for all of them. Ex., eagle_0
  -a AGO, --ago AGO     Time ago to restore to. Ex.: 24h, 1d, 86400, 1440m -
                        all the same
  -m MESSAGE, --message MESSAGE
                        Message to include in e-mail/st_ticket
  -t TICKET, --ticket TICKET
                        Number of ticket to send comment to
  -r, --run             Needed to really run
  -s {sandbox,validator}, --source {sandbox,validator}
                        Source to detect sandbox resources - Old resources
                        from sandbox or validated from validator
  -q, --quiet           Suppress some messages
  --readme              Print README.md

    Typical scenario:

      Try to rollback resources for all eagle contours
        ./resources_fallback -c eagles

      Will log actions, show changes in mentor config. WILL NOT change anything.
      If you understand, you need older resources, you can call
        ./resources_fallback -c eagles --ago 6h

      Will go deeper into history to find validated resource pack.
      If you understand, there is nothing good in validator data, you can switch to sandbox:
        ./resources_fallback -c eagles --ago 6h --sources sandbox

      Will try to resolve eagle resources descriptions, but use only resources, created earlier then 6 hours ago.
      If you are OK with the result, you can call
        ./resources_fallback -c eagles --ago 6h --sources sandbox -t BIGB-xxx -m 'OMG, we are losing money!' --run

      This will actually make changes to mentor configs!
      Ticket and message are optional, as you have no time for that during an issue resolving.
    
```
**Call `./resources_fallback --readme >> README.md` to regenerate this readme.**
