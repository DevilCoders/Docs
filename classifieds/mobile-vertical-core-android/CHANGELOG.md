# 0.21.13

Fixed merge issue

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.12...v0.21.13)


# 0.21.12

Updated AccountManager to 5.41
Fixed SegmentedGroup unsupported clip path operation

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.11...v0.21.12)


# 0.21.11

Fixed detach of RecyclerView from RecyclerViewScreenPresenter when adapter is null

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.10...v0.21.11)


# 0.21.10

Fixed bug with writing DialogItem into Parcel when DialogFragment saves its state

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.9...v0.21.10)


# 0.21.9

Dynamic screens: improve styles for TextView fields and NumberInput fields

Fixed bugs when loading pages in progress adapter

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.8...v0.21.9)


# 0.21.8

Dynamic screens: added hint for fields with values, added maxLength for number fields, 
improve SegmentedGroup widget

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.7...v0.21.8)


# 0.21.7

Added missing wrapping methods for `ProgressLoaderAdapterWraper`

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.6...v0.21.7)


# 0.21.6

Added: `CupboardProvider.registerEntityConverterFactory`, `CupboardProvider.registerFieldConverterFactory`.

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.5...v0.21.6)

# 0.21.5

[VSAPPS-2223](https://st.yandex-team.ru/VSAPPS-2223)
Disable grouping separator for decimal numbers

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.4...v0.21.5)


# 0.21.4

[VSAPPS-2281](https://st.yandex-team.ru/VSAPPS-2281)
SQLiteContentProvider didn't use id from Uri resulting in performing query/update/delete operations
on all entities instead of single one.

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.3...v0.21.4)

# 0.21.3

core: SQLiteContentProvider - use own content resolver instead of one from AppHelper, to avoid mocking AppHelper in tests.

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.2...v0.21.3)

# 0.21.2

[VSAPPS-2137](https://st.yandex-team.ru/VSAPPS-2137)
ProgressAdapterPresenter: workaround for race condition between hiding progress and updating list with new data.

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21.1...v0.21.2)

# 0.21.1

Fix fabric logger side effect.

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/v0.21...v0.21.1)

# 0.21

DialHelper clean up, updated link to Yandex apps on Google Play on About screen.

[Commits](https://github.yandex-team.ru/vertical-mobile/mobile-vertical-core-android/compare/0dfd815b8f0bad2bb88269a647f1db960c7e37ad...v0.21)
