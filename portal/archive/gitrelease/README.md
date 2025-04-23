#make release aka make\_release.pl

утилита для сборки debian/changelog
соостоит из make\_release.pl и файла конфигурации debian/relese\_utils.conf

    git submodule add git@github.yandex-team.ru:morda/gitrelease.git release_utils

cat Makefile

    release:
    	release_utils/make_release.pl --user=$(USER) 


простейщий пример конфигурации собирает 
cat debian/release\_utils.conf

    {
        flow => { 
            master => {
                release => q{master},
            },
        },
        package_version_type => 'MajorMinor'
    }
