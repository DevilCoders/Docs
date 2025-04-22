`AddressDetails` was removed from response; so, it is generated from `Address` right now.

The first version of transformation from `Address` to `AddressDetails` was created by grok@.
Tests is added to check that this transformation is correct. These tests are provided by grok@, too.

See:
 * https://st.yandex-team.ru/MAPSLIBS-135
 * https://github.yandex-team.ru/maps/libs/commit/2fa155e109671b8bbf9ee71538d6cb0e4a2c1ca4#diff-c430437f2a537c0653f754e5687bd0a7
