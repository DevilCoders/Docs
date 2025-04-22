### Version 1.15.0
[@viknet](https://staff.yandex-team.ru/viknet) Tue, 26 Feb 2019 11:57:53

 - [ADVISOR-2078](https://st.yandex-team.ru/ADVISOR-2078) trusty -> xenial

### Version 1.14.0
[@viknet](https://staff.yandex-team.ru/viknet) Wed, 09 Jan 2019 17:11:08

 - [ADVISOR-2056](https://st.yandex-team.ru/ADVISOR-2056) added extendedParams: serial_number and yphone_id

### Version 1.13.0
[@viknet](https://staff.yandex-team.ru/viknet) Fri, 28 Dec 2018 18:01:46

 - [ADVISOR-2046](https://st.yandex-team.ru/ADVISOR-2046) move localization_db and permissions_db into DBaaS

### Version 1.12.1
[@rtuaev](https://staff.yandex-team.ru/rtuaev) Tue, 25 Sep 2018 19:30:55 +0300

 - fixed set of known locales from geobase

### Version 1.12.0
[@rtuaev](https://staff.yandex-team.ru/rtuaev) Mon, 24 Sep 2018 16:24:04 +0300

 - [ADVISOR-1846](https://st.yandex-team.ru/ADVISOR-1846) changed startrek ticket id format

### Version 1.11.0
[@viknet](https://staff.yandex-team.ru/viknet) Thu, 20 Sep 2018 17:19:57

 - [ADVISOR-1852](https://st.yandex-team.ru/ADVISOR-1852) user_creation_date 'From' and 'To' conditions

### Version 1.10.0
[@viknet](https://staff.yandex-team.ru/viknet) Thu, 13 Sep 2018 15:25:03

 - [ADVISOR-1854](https://st.yandex-team.ru/ADVISOR-1854) disable creating startrek issues in stress environment

### Version 1.9.2
[@viknet](https://staff.yandex-team.ru/viknet) Mon, 10 Sep 2018 15:23:21 +0300

 - [ADVISOR-1843](https://st.yandex-team.ru/ADVISOR-1843) validate conditions.time field

### Version 1.9.1
[Viktor Druchinin](https://staff.yandex-team.ru/viknet) Tue, 21 Aug 2018 18:05:05 +0300

 - added extended parameters: os_name, min_os_version, max_os_version
 - fixed displaying help_text for fields

### Version 1.9.0
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Tue, 07 Aug 2018 15:49:10 +0300

 - storing and using locales in db
 - switching between environments from menu
 - added helpstrings for all controls

### Version 1.8.0
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Wed, 25 Jul 2018 13:45:31 +0300

 - [ADVISOR-1703](https://st.yandex-team.ru/ADVISOR-1703): added geo targeting
 - fixed bug modification list of values
 - removed country_init field

### Version 1.7.0
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Thu, 28 Jun 2018 19:56:32 +0300

 - [ADVISOR-1692](https://st.yandex-team.ru/ADVISOR-1692): changed clid value from one value to list of values

### Version 1.6.2
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Wed, 13 Jun 2018 15:47:57 +0300

 - fix for creation date

### Version 1.6.1
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Tue, 15 May 2018 18:02:46 +0300

 - added clids validation

### Version 1.6.0
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Fri, 27 Apr 2018 21:25:10 +0300

 - implemented creation of doc diff into Startrek ticket comments

### Version 1.5.0
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Thu, 26 Apr 2018 15:30:10 +0300

 - added Open StarTrek link to list and edit form

### Version 1.4.2
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Wed, 24 Apr 2018 18:00:10 +0300

 - fix Dockerfile

### Version 1.4.1
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Tue, 24 Apr 2018 13:40:14 +0300

 - fix: removing updated_at value if present
 - find issue which have the same summary exactly (not substring)
 - added reference to user/environment type in the comment

### Version 1.4.0
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Wed, 18 Apr 2018 16:36:14 +0300

 - implemented integration experiments & Startrek [ADVISOR-1452]
 - moved sensitive data into secrets
 - implemented export/import feature for documents (move data between environments)

### Version 1.3.2
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Fri, 13 Apr 2018 16:00:00 +0300

 - fixed datetime correction using actual timezone

### Version 1.3.1
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Wed, 4 Apr 2018 13:20:45 +0300

 - new pymongo and hardcoded db name fixes

### Version 1.3.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 3 Apr 2018 13:20:45 +0300

 - new mongo settings
 - added using mongos

### Version 1.2.0
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Wed, 14 Feb 2018 13:20:45 +0300

 - added Updated_at field

### Version 1.1.6
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Mon, 2 Feb 2018 16:40:07 +0300

 - fix flask versions

### Version 1.1.5
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 24 Oct 2017 16:40:07 +0300

 - oauth authorization 
 - remove debian deploy settings 
 - docker deploy and remove some code

### Version 1.1.3
[Aleksandr Igoshkin](https://staff.yandex-team.ru/igoshkin) Mon, 15 Jan 2018 15:37:14 +0300

 - fix empty grep results in fab

### Version 1.1.2
[Aleksandr Igoshkin](https://staff.yandex-team.ru/igoshkin) Thu, 14 Dec 2017 13:40:14 +0300

 - fix mongo settings

### Version 1.1.1
[Anton Grigoryev](https://staff.yandex-team.ru/griganton) Tue, 24 Oct 2017 16:40:07 +0300

 - add placement to extended params

### Version 1.1.0
[Roman Tuaev](https://staff.yandex-team.ru/rtuaev) Tue, 12 Sep 2017 19:15:07 +0300

 - fixed mongodb hosts for stress environment

### Version 1.0.1
[Aleksandr Igoshkin](https://staff.yandex-team.ru/igoshkin) Mon, 17 Jul 2017 19:31:38 +0300

 - fix path to /static in nginx conf

### Version 1.0.0
[Aleksandr Igoshkin](https://staff.yandex-team.ru/igoshkin) Wed, 28 Jun 2017 15:08:04 +0300

 - Initial release
