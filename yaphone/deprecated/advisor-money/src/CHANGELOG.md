
### Version 0.29.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 18 Dec 2018 19:18:26 +0300

 - [ZEN-17070](https://st.yandex-team.ru/ZEN-17070): added new partner Microsoft

### Version 0.29.2
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Wed, 21 Nov 2018 18:04:22 +0300

 - RequirementViolatedError fix

### Version 0.29.1
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Wed, 21 Nov 2018 16:04:22 +0300

 - [ADVISOR-1982](https://st.yandex-team.ru/ADVISOR-1982): upgrade nile

### Version 0.29.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 21 Nov 2018 15:54:30 +0300

 - [ZEN-16844](https://st.yandex-team.ru/ZEN-16844)/16845: different revenue_share for different platforms

### Version 0.28.10
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 19 Nov 2018 18:15:25 +0300

 - [ADVISOR-1970](https://st.yandex-team.ru/ADVISOR-1970): don't overwrite non-zero data with zero values in partner reports

### Version 0.28.9
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 13 Nov 2018 17:34:12 +0300

 - [ZEN-16649](https://st.yandex-team.ru/ZEN-16649): new partner RussiaOperaBrowser

### Version 0.28.8
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 22 Oct 2018 20:08:20 +0300

 - [ADVISOR-1909](https://st.yandex-team.ru/ADVISOR-1909): hasoffers_conversions script now finds installs by HasOffers ID

### Version 0.28.7
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 09 Oct 2018 11:09:14 +0300

 - [ZEN-15560](https://st.yandex-team.ru/ZEN-15560): added new partner Sony

### Version 0.28.6
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 08 Oct 2018 14:41:36 +0300

 - [ZEN-15540](https://st.yandex-team.ru/ZEN-15540): added new partner MeizuZenkit2
 - Fixed Dip partner's discovery_clid

### Version 0.28.5
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 04 Oct 2018 15:32:36 +0300

 - fixed bug in load_clids script

### Version 0.28.4
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 01 Oct 2018 14:28:47 +0300

 - added Dip partner

### Version 0.28.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 17 Sep 2018 12:08:22 +0300

 - added cli function call if __name__ == '__main__'
 - refactored PartnerReportUpdater (added run() method)
 - logging error if no activations for FlyHigh and FlyLow

### Version 0.28.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 08 Aug 2018 15:05:12 +0300

 - Hitlog for 5 days and logging error if impression_id is null

### Version 0.28.1
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Thu, 02 Aug 2018 13:15:00 +0300

 - Hitlog for 2 days

### Version 0.28.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Thu, 02 Aug 2018 10:40:35 +0300

 - [ADVISOR-1480](https://st.yandex-team.ru/ADVISOR-1480): parse direct postbacks

### Version 0.27.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 30 Jul 2018 12:17:21 +0300

 - changed Distribution API url

### Version 0.27.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 27 Jul 2018 18:25:16 +0300

 - Meizu partner changed conditions

### Version 0.27.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 12 Jul 2018 16:29:33 +0300

 - [ZEN-13310](https://st.yandex-team.ru/ZEN-13310): DexpApprec partner changed to Dexp (now computing Apprec and Zen)

### Version 0.27.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 10 Jul 2018 18:40:35 +0300

 - [ADVISOR-1742](https://st.yandex-team.ru/ADVISOR-1742): Hasoffers conversions fixes

### Version 0.26.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 28 Jun 2018 15:41:56 +0300

 - [ADVISOR-1694](https://st.yandex-team.ru/ADVISOR-1694): stop writing to old money report tables

### Version 0.26.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 19 Jun 2018 14:49:30 +0300

 - [ADVISOR-1668](https://st.yandex-team.ru/ADVISOR-1668): Nile-based postback parser + ensure right adnetwork

### Version 0.25.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Thu, 14 Jun 2018 16:30:58 +0300

 - [ZEN-12578](https://st.yandex-team.ru/ZEN-12578) added new partners
 - [ZEN-12309](https://st.yandex-team.ru/ZEN-12309) added vvp to partners

### Version 0.24.4
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 07 Jun 2018 08:05:44 +0300

 - fixed rec_launch event in hasoffer_conversions

### Version 0.24.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 06 Jun 2018 13:08:36 +0300

 - renamed rec_app_launch event to rec_launch

### Version 0.24.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 06 Jun 2018 10:50:27 +0300

 - uploading custom conversions to hasoffers in testing env

### Version 0.24.1
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 24 Apr 2018 13:06:16 +0300

 - limit pip version

### Version 0.24.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 19 Apr 2018 16:26:21 +0300

 - refactored partner_reports script
 - summing partner's revenue and only then converting
 - added new partners FlyHigh, FlyLow, Dexp

### Version 0.23.6
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 10 Apr 2018 14:22:03 +0300

 - fixed big with importing HASOFFERS_API_TOKEN

### Version 0.23.5
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 10 Apr 2018 11:34:13 +0300

 - removed secrets from repo

### Version 0.23.4
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 09 Apr 2018 13:07:16 +0300

 - writing money reports to closed directory in YT

### Version 0.23.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 04 Apr 2018 10:13:07 +0300

 - fixed CLIDS_JSON_FILE path

### Version 0.23.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 02 Apr 2018 12:45:43 +0300

 - updated yandex-currency-converter to 0.1.4

### Version 0.23.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 30 Mar 2018 12:30:28 +0300

 - added new partner ZteZenApp

### Version 0.23.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Fri, 23 Mar 2018 10:57:39 +0300

 - [ADVISOR-1513](https://st.yandex-team.ru/ADVISOR-1513): New Sentry

### Version 0.22.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 01 Mar 2018 13:53:00 +0300

 - added new partner HolaZenkit

### Version 0.22.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 15 Feb 2018 09:32:04 +0300

 - Added new partner Huawei

### Version 0.22.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Wed, 14 Feb 2018 13:09:45 +0300

 - [ADVISOR-1513](https://st.yandex-team.ru/ADVISOR-1513): New Sentry

### Version 0.21.8
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 02 Feb 2018 20:10:18 +0300

 - fixed advisor_replica_db settings

### Version 0.21.7
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 01 Feb 2018 14:54:05 +0300

 - fixed error with promo_event_tables in parse_postbacks

### Version 0.21.6
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 31 Jan 2018 10:18:36 +0300

 - Changed yt tables path //stabox -> //home/logfeller

### Version 0.21.5
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 31 Jan 2018 10:02:16 +0300

 - Fixed bug with missing impression_id in metrika-mobile-log

### Version 0.21.4
[Artem Khurshudov](https://staff.yandex-team.ru/anglerfish) Fri, 26 Jan 2018 18:51:33 +0300

 - fixing Friday bug from the last commit

### Version 0.21.3
[Artem Khurshudov](https://staff.yandex-team.ru/anglerfish) Fri, 26 Jan 2018 18:28:00 +0300

 - removing zklock wrapper from monitoring command

### Version 0.21.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 26 Jan 2018 11:14:58 +0300

 - removed lookback argument from partner_reports script

### Version 0.21.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 22 Jan 2018 08:50:19 +0300

 - deleted Zenkit ackivations script

### Version 0.21.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Sat, 20 Jan 2018 17:39:48 +0300

 - using Click framework for cli commands

### Version 0.20.5
[Islam Alibekov](https://staff.yandex-team.ru/everest) Sat, 20 Jan 2018 17:01:24 +0300

 - added new partner Meizu (Zenkit)

### Version 0.20.4
[Artem Khurshudov](https://staff.yandex-team.ru/anglerfish) Fri, 19 Jan 2018 12:31:49 +0300

 - disabling logging for monrun settings

### Version 0.20.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 18 Jan 2018 11:43:00 +0300

 - updated yandex-currency-converter package to 0.1.3

### Version 0.20.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 11 Dec 2017 08:39:06 +0300

 - rewrite hasoffers_conversions

### Version 0.20.1
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Thu, 07 Dec 2017 16:02:53 +0300

 - decode pluses in postback to spaces

### Version 0.20.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 28 Nov 2017 18:58:45 +0300

 - matching conversions from metrika and uploading them to HasOffers

### Version 0.19.7
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 13 Nov 2017 12:14:27 +0300

 - fixed postback_is_testing function

### Version 0.19.6
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Thu, 09 Nov 2017 16:45:14 +0300

 - fix: added settings.py & default_settings.py files for YT jobs

### Version 0.19.5
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 08 Nov 2017 09:41:15 +0300

 - skipping testing postbacks when parsing access log

### Version 0.19.4
[Islam Alibekov](https://staff.yandex-team.ru/everest) Sat, 04 Nov 2017 10:28:34 +0300

 - merged hotfix frm master (0.18.6.1) to develop

### Version 0.19.3
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Wed, 01 Nov 2017 11:52:03 +0300

 - fix monitoring logging

### Version 0.19.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 27 Oct 2017 11:07:53 +0300

 - fixed monthly offer_stats

### Version 0.19.1
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Wed, 25 Oct 2017 22:20:43 +0300

 - hotfix: fixed run jobs inside YT

### Version 0.19.0
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Wed, 25 Oct 2017 19:48:02 +0300

 - added user_settings module to be able run commands by hands + some refactoring

### Version 0.18.6.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Sat, 04 Nov 2017 10:10:01 +0300

 - updated yacurrency package version

### Version 0.18.6
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 19 Oct 2017 17:02:46 +0300

 - fixed problem with missing postbacks in mongo
 - added ipython to requirements
 - refactored mongo URIs

### Version 0.18.5
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 19 Oct 2017 16:42:33 +0300

 - fixed parsing postbacks with invalid request

### Version 0.18.4
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Wed, 18 Oct 2017 21:09:12 +0300

 - fixed: do't raised exception if no ops in bulk execute method

### Version 0.18.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 11 Oct 2017 14:33:08 +0300

 - added partner MTS

### Version 0.18.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 19 Sep 2017 17:07:25 +0300

 - merge hotfix 0.17.7 from master

### Version 0.18.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 15 Sep 2017 15:29:21 +0300

 - fixed run_cmd error in promo_stats script

### Version 0.18.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 15 Sep 2017 14:37:17 +0300

 - Parsing Postbacks using data from mongo
 - Calculating PromoOfferStats every 15 min

### Version 0.17.7
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 19 Sep 2017 17:05:14 +0300

 - fixed clids url on YT

### Version 0.17.6
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 01 Aug 2017 14:14:31 +0300

 - added support for dynamic configuration of direct adnetworks

### Version 0.17.5
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 24 Jul 2017 21:14:32 +0300

 - added postback parsing for direct-stroer

### Version 0.17.4
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 21 Jul 2017 09:59:59 +0300

 - fixed chmod in postinst

### Version 0.17.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 20 Jul 2017 14:40:36 +0300

 - fixed payout_unconverted and currency fields in parse_postbacks

### Version 0.17.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 19 Jul 2017 18:50:46 +0300

 - one more try to fix monrun crashing

### Version 0.17.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 19 Jul 2017 16:56:39 +0300

 - fixed parse_postbacks tetst

### Version 0.17.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 19 Jul 2017 16:34:03 +0300

 - added non USD offers support

### Version 0.16.4
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 19 Jul 2017 12:41:11 +0300

 - fixed adnetwork name parsing from postback

### Version 0.16.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 19 Jul 2017 09:09:12 +0300

 - Added postback parsing for DirectPlarium

### Version 0.16.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 18 Jul 2017 10:45:06 +0300

 - each script has its own log file

### Version 0.16.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 17 Jul 2017 21:54:59 +0300

 - fixed monrun "Can't parse output" problem

### Version 0.16.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 17 Jul 2017 20:38:05 +0300

 - added new partner ZapZap

### Version 0.15.7
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 17 Jul 2017 15:00:39 +0300

 - fixed zookeper host

### Version 0.15.6
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 29 Jun 2017 16:42:24 +0300

 - collecting impression_id from Cheetah's postback params

### Version 0.15.5
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 21 Jun 2017 09:11:02 +0300

 - splited Multilaser revenue (phone and tablet)

### Version 0.15.4
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 19 Jun 2017 21:33:10 +0300

 - country parameter fixed for Multilaser

### Version 0.15.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 19 Jun 2017 21:22:20 +0300

 - added country_geo_id check for Multilaser

### Version 0.15.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 19 Jun 2017 21:01:26 +0300

 - fixed partners/__init__.py

### Version 0.15.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 19 Jun 2017 20:53:32 +0300

 - fixed partner-reports path

### Version 0.15.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 19 Jun 2017 20:49:56 +0300

 - added new partner Multilaser (Browser)

### Version 0.14.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 16 Jun 2017 12:12:45 +0300

 - added new partner Posh Mobile

### Version 0.13.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 13 Jun 2017 14:35:43 +0300

 - added new partner Lava (exclusive / non-exclusive)

### Version 0.12.18
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 12 Jun 2017 10:03:21 +0300

 - added new build-requirements

### Version 0.12.17
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 12 Jun 2017 09:33:18 +0300

 - fixed settings.py and requirements

### Version 0.12.16
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 09 Jun 2017 15:32:45 +0300

 - fixed postback parsing for Cheetah

### Version 0.12.15
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 07 Jun 2017 17:39:41 +0300

 - fixed revenue from DIR (using only 50%)

### Version 0.12.14
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Mon, 05 Jun 2017 15:07:39 +0300

 - clickhouse fix

### Version 0.12.13
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 05 Jun 2017 14:47:18 +0300

 - fixed settings.py crashed by previous commit

### Version 0.12.12
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 05 Jun 2017 14:44:53 +0300

 - fixed postback parsing for Mundomedia

### Version 0.12.11
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 05 Jun 2017 11:17:11 +0300

 - Added Wileyfox, C Launcher and made minor fixes to scripts

### Version 0.12.10
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 01 Jun 2017 13:19:35 +0300

 - fixed table exist check

### Version 0.12.9
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 01 Jun 2017 12:31:20 +0300

 - Added time check for zen table exist in partners_report

### Version 0.12.8
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 31 May 2017 21:41:35 +0300

 - added Wargaming and Fly revshare partners

### Version 0.12.7
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 30 May 2017 17:51:17 +0300

 - updated requiremets.in (using new version of yacurrency)

### Version 0.12.6
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 25 May 2017 23:01:06 +0300

 - fixed postback parsing for Unilead and added it for Gameberry

### Version 0.12.5
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 25 May 2017 15:46:27 +0300

 - postback parsing for Rocket10 and Mundomedia

### Version 0.12.4
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 22 May 2017 15:18:21 +0300

 - enoe more fix of scripts' parsing arguments on import

### Version 0.12.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 22 May 2017 14:45:06 +0300

 - fixed scripts' parsing arguments on import

### Version 0.12.2
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Mon, 22 May 2017 13:15:39 +0300

 - [ADVISOR-1046](https://st.yandex-team.ru/ADVISOR-1046) fix

### Version 0.12.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 19 May 2017 18:35:43 +0300

 - monitoring is not so paranoic now

### Version 0.12.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 18 May 2017 17:52:01 +0300

 - partners_report script writes daily revenue diffs

### Version 0.11.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Wed, 17 May 2017 16:19:09 +0300

 - use device_id instead android_id in postbacks report [ADVISOR-1046](https://st.yandex-team.ru/ADVISOR-1046)

### Version 0.10.7
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 17 May 2017 07:39:54 +0300

 - Many little fixes to advisor_money.scripts

### Version 0.10.6
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Mon, 15 May 2017 18:42:00 +0300

 - fix postbacks reports path

### Version 0.10.5
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Mon, 15 May 2017 17:35:49 +0300

 - upgrade yandex-yt

### Version 0.10.4
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 12 May 2017 10:21:04 +0300

 - fixed logging settings

### Version 0.10.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 10 May 2017 12:00:04 +0300

 - fixed date argument in partners-report script

### Version 0.10.2
[Artem Khurshudov](https://staff.yandex-team.ru/anglerfish) Wed, 10 May 2017 11:18:26 +0300

 - switching back to Hahn cluster

### Version 0.10.1
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Fri, 05 May 2017 15:30:26 +0300

 - fix date_utils

### Version 0.10.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Thu, 04 May 2017 15:50:17 +0300

 - add device_id tp postbacks [ADVISOR-1035](https://st.yandex-team.ru/ADVISOR-1035)

### Version 0.9.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 28 Apr 2017 15:02:37 +0300

 - fixed date argument parsing in scripts/__init__.py

### Version 0.9.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 27 Apr 2017 21:09:59 +0300

 - Added partner report for Micromax

### Version 0.8.6
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 27 Apr 2017 17:17:51 +0300

 - added partners report calculating

### Version 0.8.5
[Artem Khurshudov](https://staff.yandex-team.ru/anglerfish) Wed, 26 Apr 2017 20:23:23 +0300

 - switching to Banach cluster

### Version 0.8.4
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 20 Apr 2017 18:40:02 +0300

 - fixed monrun monitoring script

### Version 0.8.3
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Thu, 13 Apr 2017 11:34:07 +0300

 - change clickhouse host to mtsmart

### Version 0.8.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 12 Apr 2017 11:11:17 +0300

 - fixed monrun monitoring script

### Version 0.8.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 07 Apr 2017 13:45:15 +0300

 - moved currency converter to standalone python package

### Version 0.8.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Thu, 06 Apr 2017 18:29:09 +0300

 - added CurrencyConverter

### Version 0.7.4
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Mon, 03 Apr 2016 14:13:13 +0300

 - add requests to requirements implicitly

### Version 0.7.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 31 Mar 2017 15:20:08 +0300

 - fixed monrun/advisor-money.conf

### Version 0.7.2
[Islam Alibekov](https://staff.yandex-team.ru/everest) Wed, 29 Mar 2017 14:50:24 +0300

 - replacing invalid clid with -2 in postbacks_report

### Version 0.7.1
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 28 Mar 2017 12:22:41 +0300

 - fixed AppLift postback parsing

### Version 0.7.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 24 Mar 2017 19:52:54 +0300

 - updated monitoring for money reports

### Version 0.6.0
[Aleksandr Igoshkin](https://staff.yandex-team.ru/igoshkin) Thu, 09 Mar 2017 19:38:11 +0300

 - Add filtration by yandex ip's [ADVISOR-829](https://st.yandex-team.ru/ADVISOR-829)

### Version 0.5.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 03 Mar 2017 14:39:33 +0300

 - added monitoring for money reports

### Version 0.4.0
[Islam Alibekov](https://staff.yandex-team.ru/everest) Fri, 03 Mar 2017 14:08:24 +0300

 - saving zenkit scroll_down events to YT [ADVISOR-895](https://st.yandex-team.ru/ADVISOR-895)

### Version 0.3.8
[Islam Alibekov](https://staff.yandex-team.ru/everest) Mon, 27 Feb 2017 20:01:39 +0300

 - postback reports created by day and saved to adnetwork-postbacks-reports/

### Version 0.3.7
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Sat, 18 Feb 2016 11:59:11 +0300

 - fix: null offer id processing

### Version 0.3.6
[Islam Alibekov](https://staff.yandex-team.ru/everest) Sat, 18 Feb 2017 10:56:54 +0300

 - fixed postback parsing for Mobupps

### Version 0.3.5
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Mon, 13 Feb 2016 15:08:10 +0300

 - fix: ignore non-ascii symbols in device manufacturer/model

### Version 0.3.4
[Dmitry Kaluzhny](https://staff.yandex-team.ru/dmitryka) Fri, 03 Feb 2017 15:30:45 +0300

 - do not crash in case of misformatted payout in postback request

### Version 0.3.3
[Islam Alibekov](https://staff.yandex-team.ru/everest) Tue, 24 Jan 2017 15:27:10 +0300

 - fixed postback parsing for IronSource adnetwork

### Version 0.3.2
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Fri, 20 Jan 2016 10:44:00 +0300

 - fix: script run times

### Version 0.3.1
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Thu, 19 Jan 2016 15:34:00 +0300

 - fix: ignore invalid log records

### Version 0.3.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Wed, 18 Jan 2016 17:12:00 +0300

 - postbacks report [ADVISOR-801](https://st.yandex-team.ru/ADVISOR-801)

### Version 0.2.6
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 18 Jan 2016 14:53:00 +0300

 - save postbacks for 90 days

### Version 0.2.5
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 17 Jan 2016 16:32:00 +0300

 - 30 days of promoevents
 - get info only from las promoevent

### Version 0.2.4
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 17 Jan 2016 15:13:00 +0300

 - fix table naming

### Version 0.2.2
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 17 Jan 2016 14:24:00 +0300

 - fix jobs failing

### Version 0.2.1
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 17 Jan 2016 13:46:00 +0300

 - fix tests and set payout from promo_event

### Version 0.2.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 17 Jan 2016 13:45:00 +0300

 - Move promoevents to YT

### Version 0.1.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Mon, 15 Dec 2016 17:05:00 +0300

 - Parse postbacks script

### Version 0.0.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Mon, 12 Dec 2016 21:17:17 +0300

 - Initial release.
