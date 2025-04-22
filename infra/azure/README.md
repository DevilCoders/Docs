# Terraform RTC scripts
## Requirements
* installed azure cli (https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* installed terraform latest stable binary (https://hashicorp-releases.website.yandexcloud.net/terraform/)
* configured terraform to use yandex-cloud mirror (https://cloud.yandex.ru/docs/tutorials/infrastructure-management/terraform-quickstart#configure-provider)
* installed and configured (logged in) dns-monkey.pl accessible in PATH (https://wiki.yandex-team.ru/dynamic-dns/dns-monkey-roadmap/)
* obtained and available via env WALLE_TOKEN (obtain at https://oauth.yandex-team.ru/authorize?response_type=token&client_id=9e9702c0b7f54152ac339989d9039ccd)
* ssh-key at staff for certctl certificate deploy (add to ssh agent unlocked, without password prompt)
