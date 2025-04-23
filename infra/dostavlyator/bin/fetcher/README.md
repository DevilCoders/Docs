# fetcher

Basic fetcher implementation

## to be done

- CHECKSUM_BROKEN/DOWNLOADING - do not remove in cleanup, process in fetch_rbtorrent
- TBoxAppliedSpec.Resource.Status => TBoxAppliedSpec.Resource.ValidationStatus
- fix https://a.yandex-team.ru/arc_vcs/infra/dostavlyator/bin/fetcher/__main__.py?rev=9e80fcc1b862edb7fc87ce5a018c2bb5d53e0223#L133 - sync ValidationStatus from box_applied to local_box_applied, then assign box_applied.Resource = local_box_applied.Resource?
- drop stale processes
- custom priority support?
- solomon metrics
- async?
