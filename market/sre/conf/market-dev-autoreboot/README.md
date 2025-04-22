# market-dev-autoreboot
CSADMIN-41584 На машинах logrus и devrep сделать панику и автоперезагрузку после софтлоков, хардлоков, упсов. На OOM-ы решено не ребутитьтся, а защитить ssh (sshd, sssd, systemd-logind) от OOM-ов.
