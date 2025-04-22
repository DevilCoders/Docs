# NAME

cron\_errs - check cron errors reports

# DESCRIPTION

When command in crontab fail or print to STDERR/STDOUT cron daemon send email
to command's owner. RTC can't afford to send email for each error on every host
in the fleet, so emails for crontabs are disabled. At the same time such emails
are only alerts about problems in crontabs, hence this emails are redirected
to file `/var/log/fs_mail/fs_mail.dump` to give ability to monitor and diagnose
this kind of problems.

Note: `/var/log/fs_mail/fs_mail.dump` is rotated by logrotate.

# SEVERITY

Low.

# DIAGNOSTICS

    tail -100 /var/log/fs_mail/fs_mail.dump

# FAST FIX

None.

# KNOWN ISSUES

[HOSTMAN-150](https://st.yandex-team.ru/HOSTMAN-150)  
[HOSTMAN-151](https://st.yandex-team.ru/HOSTMAN-151)  

# RESPONSIBLE

[SRE RTC](https://staff.yandex-team.ru/departments/yandex_mnt_sa_runtime_cross/)

# RELATED TICKETS

[HOSTMAN-57](https://st.yandex-team.ru/HOSTMAN-57)  
[RUNTIMECLOUD-2079](https://st.yandex-team.ru/RUNTIMECLOUD-2079)  
