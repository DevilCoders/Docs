# NAME

ll_duplicate_addr

# DESCRIPTION

Find duplicate LL address.

# SEVERITY

Critical.

# DIAGNOSTICS

	# Getting curent LL address for MTN interface (vlan688 or vlan788)
	ll=$(ip a s dev vlan688 | grep "scope link" | grep "fe80::a:" | awk '{print $2}' | sed -e 's/\/64//')

	# Finding duplicate in network through Neighbor Discovery protocol
	/usr/bin/ndisc6 -n -r 1 $ll vlan688

	If previous command return "No response" it means duplicates on network not found. Otherwise we have a problem.


# RESPONSIBLE

[SYSDEV](https://staff.yandex-team.ru/departments/yandex_mnt_sa_runtime_mondev_6921/)
