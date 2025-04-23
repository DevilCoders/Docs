yamail-network-scripts (1.0.33) testing; urgency=low

  * [MAILSRE-927] Disable PMTU

 -- David Mushailov <damoka@yandex-team.ru> Fri, 24 Dec 2021 16:30:00 +0300

yamail-network-scripts (1.0.32) testing; urgency=low

  * Add multi chain report for slb_reject

 -- Petr Burmistrov <pierre@yandex-team.ru>  Tue, 16 Feb 2021 00:08:56 +0300

yamail-network-scripts (1.0.31) testing; urgency=low

  * purge yandex-netconfig

 -- Petr Burmistrov <pierre@yandex-team.ru>  Tue, 16 Feb 2021 00:08:56 +0300

yamail-network-scripts (1.0.30) testing; urgency=low

  * specify yandex-hbf-agent-monitoring version

 -- Petr Burmistrov <pierre@yandex-team.ru>  Tue, 16 Feb 2021 00:08:56 +0300


yamail-network-scripts (1.0.29) testing; urgency=low

  * specify yandex-hbf-agent-monitoring version

 -- Petr Burmistrov <pierre@yandex-team.ru>  Tue, 16 Feb 2021 00:08:56 +0300

yamail-network-scripts (1.0.28) testing; urgency=low

  * fix drills 

 -- Petr Burmistrov <pierre@yandex-team.ru> Thu, 30 May 2019 14:56:42 +0300

yamail-network-scripts (1.0.27) testing; urgency=low

  * [MAILDLV-5006] Make balancer_reject critcal when drills

 -- Petr Burmistrov <pierre@yandex-team.ru> Thu, 30 May 2019 14:56:42 +0300

yamail-network-scripts (1.0.26) testing; urgency=low

  * [MAILDLV-3866] Fix fw rules install path

 -- Petr Burmistrov <pierre@yandex-team.ru> Thu, 30 May 2019 14:56:42 +0300

yamail-network-scripts (1.0.25) testing; urgency=low

  * [MAILDLV-3866] Added fw rules links for hbf-agent 

 -- Petr Burmistrov <pierre@yandex-team.ru> Thu, 30 May 2019 14:56:42 +0300

yamail-network-scripts (1.0.24) testing; urgency=low

  * BIND: set ipv6-only forwarders

 -- Petr Burmistrov <pierre@yandex-team.ru> Thu, 30 May 2019 14:56:42 +0300

yamail-network-scripts (1.0.23) testing; urgency=low

  * [MAILDLV-2971] Added notification if error while balancer manage

 -- Petr Burmistrov <pierre@yandex-team.ru> Fri, 24 May 2019 15:00:39 +0300

yamail-network-scripts (1.0.22) testing; urgency=low

  * fix install

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 24 Apr 2019 20:13:31 +0300

yamail-network-scripts (1.0.21) testing; urgency=low

  * [MAILDLV-2482] Added generator ipv4 tunel interface

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 24 Apr 2019 19:46:06 +0300

yamail-network-scripts (1.0.20) testing; urgency=low

  * Added sleep to network-setup.sh

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 16 Jan 2019 17:51:32 +0300

yamail-network-scripts (1.0.19) testing; urgency=low

  * Added network-setup.sh for setup network in setup.yandex-team.ru

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 16 Jan 2019 02:23:59 +0300

yamail-network-scripts (1.0.18) testing; urgency=low

  * Add SHELL=/bin/bash for random sleep in cron

 -- Petr Burmistrov <pierre@yandex-team.ru> Mon, 24 Dec 2018 20:06:20 +0300

yamail-network-scripts (1.0.17) testing; urgency=low

  * update postinstall

 -- Petr Burmistrov <pierre@yandex-team.ru> Tue, 13 Nov 2018 21:17:09 +0300

yamail-network-scripts (1.0.16) testing; urgency=low

  *  Update slb monitoring
  *  Added yandex-juggler-conntrackissmall-check to deps
  *  Rewrite manage-balancer to work more graceful
  *  Add hfb to deps

 -- Petr Burmistrov <pierre@yandex-team.ru> Tue, 13 Nov 2018 20:45:31 +0300

yamail-network-scripts (1.0.15) testing; urgency=low

  *  Fix error "maximum number of FD events" in named
  *  [IMAPINCIDENTS-5] Reverting conntrack in crond after reboot

 -- Petr Burmistrov <pierre@yandex-team.ru> Tue, 09 Oct 2018 01:25:15 +0300

yamail-network-scripts (1.0.13) testing; urgency=low

  * Apply conntrack in postinstall

 -- Petr Burmistrov <pierre@yandex-team.ru> Tue, 18 Sep 2018 21:17:24 +0300

yamail-network-scripts (1.0.12) testing; urgency=low

  * update monrun check name: balancer_reject

 -- Petr Burmistrov <pierre@yandex-team.ru> Thu, 02 Aug 2018 21:39:51 +0300

yamail-network-scripts (1.0.11) testing; urgency=low

  * fix install

 -- Petr Burmistrov <pierre@yandex-team.ru> Tue, 31 Jul 2018 19:35:42 +0300

yamail-network-scripts (1.0.10) testing; urgency=low

  * add tun_reject monrun check

 -- Petr Burmistrov <pierre@yandex-team.ru> Tue, 31 Jul 2018 18:41:01 +0300

yamail-network-scripts (1.0.9) testing; urgency=low

  * fix ip6tnl0 interface in manage-balancer

 -- Petr Burmistrov <pierre@yandex-team.ru> Thu, 28 Jun 2018 14:02:10 +0300

yamail-network-scripts (1.0.8) testing; urgency=low

  * fix ip6tnl0 interface in manage-balancer

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 27 Jun 2018 18:10:26 +0300

yamail-network-scripts (1.0.7) testing; urgency=low

  * MPROTO-4395 Rewrite manage-balancer to bash with HBF support

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 27 Jun 2018 17:23:31 +0300

yamail-network-scripts (1.0.6) testing; urgency=low

  * add 95-conntrack.conf

 -- Petr Burmistrov <pierre@yandex-team.ru> Thu, 03 May 2018 21:51:49 +0300

yamail-network-scripts (1.0.5) testing; urgency=low

  * ver++

 -- Petr Burmistrov <pierre@yandex-team.ru> Thu, 25 Jan 2018 22:15:50 +0300

yamail-network-scripts (1.0.4) testing; urgency=low

  * optimize manage-balancer for working with hbf-agent

 -- Petr Burmistrov <pierre@yandex-team.ru> Thu, 25 Jan 2018 21:55:25 +0300

yamail-network-scripts (1.0.3) testing; urgency=low

  * update get ip API url

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 18 Oct 2017 18:29:27 +0300

yamail-network-scripts (1.0.2) testing; urgency=low

  * add Conflicts: avahi-autoipd

 -- Petr Burmistrov <pierre@yandex-team.ru> Fri, 14 Apr 2017 19:30:19 +0300

yamail-network-scripts (1.0.1) testing; urgency=low

  * add postinst

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 28 Dec 2016 17:28:54 +0300

yamail-network-scripts (1.0.0) testing; urgency=low

  * add bind configs

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 28 Dec 2016 17:24:38 +0300

yamail-network-scripts (0.0.12) testing; urgency=low

  * update detecting tunel balancer

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 07 Dec 2016 21:38:31 +0300

yamail-network-scripts (0.0.11) testing; urgency=low

  * update definding ext IP address

 -- Petr Burmistrov <pierre@yandex-team.ru> Mon, 10 Oct 2016 14:16:13 +0300

yamail-network-scripts (0.0.10) testing; urgency=low

  * ver++

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 07 Sep 2016 19:22:55 +0300

yamail-network-scripts (0.0.9) testing; urgency=low

  * remove config-interfaces from deps

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 07 Sep 2016 19:12:37 +0300

yamail-network-scripts (0.0.8) testing; urgency=low

  * fix resolv.conf chattr

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 06 Jul 2016 17:33:34 +0300

yamail-network-scripts (0.0.7) testing; urgency=low

  * fix resolv.conf

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 06 Jul 2016 17:27:47 +0300

yamail-network-scripts (0.0.6) testing; urgency=low

  * udpate resolv.conf

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 06 Jul 2016 15:48:53 +0300

yamail-network-scripts (0.0.5) testing; urgency=low

  * rewrite update-network
  * add manage-balancer
  * add desc to control

 -- Petr Burmistrov <pierre@yandex-team.ru> Wed, 06 Jul 2016 15:39:16 +0300

yamail-network-scripts (0.0.4) testing; urgency=low

  * rewrite update-network

 -- Petr Burmistrov <pierre@yandex-team.ru> Tue, 28 Jun 2016 15:52:50 +0300

yamail-network-scripts (0.0.3) testing; urgency=low

  * add lucid support

 -- Petr Burmistrov <pierre@ynadex-team.ru>  Thu, 19 Mar 2015 18:49:03 +0300

yamail-network-scripts (0.0.2) testing; urgency=low

  * add generate_balancer

 -- Petr Burmistrov <pierre@ynadex-team.ru>  Thu, 19 Mar 2015 14:50:45 +0300

yamail-network-scripts (0.0.1) testing; urgency=low

  * Initial release (Closes: #nnnn)  <nnnn is the bug number of your ITP>

 -- Petr Burmistrov <pierre@ynadex-team.ru>  Fri,28 Apr 2014 13:05:24 +0400
