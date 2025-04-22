Change Log
==========

Version 0.6.0 *(2020-04-02)*
----------------------------
 * New: YS Display fonts

Version 0.5.0 *(2019-09-06)*
----------------------------
 * Updated: Migration to AndroidX #114
 * Updated: Gradle plugin updated to 3.3.0 #114
 * Updated: Gradle updated to 4.10.3 #114

Version 0.4.0 *(2019-02-09)*
----------------------------

 * Updated: Compile sdk version updated to 28 #110
 * Updated: Support library updated to 28.0.0 #110
 * Updated: Gradle plugin updated to 3.2.0 #110
 * Updated: Gradle updated to 4.7 #110
 * Fix: Attribute textColorError changed to errorTextAppearance #110

Version 0.3.4 *(2018-12-04)*
----------------------------

 * Updated: Update fonts to 180719 (https://st.yandex-team.ru/DSGN-13542) #111

Version 0.3.3 *(2018-10-12)*
----------------------------

 * New: Split fonts library into separate artifacts with single font file #108

Version 0.3.2 *(2017-12-13)*
----------------------------

 * Updated: Allow using textStyle="bold" for texts with regular YS font #105

Version 0.3.1 *(2017-11-27)*
----------------------------

 * New: Update fonts to YS Text `Version 1.1 2017` (use `otfinfo --info *.ttf | grep Version` to verify) #99
 * Updated: Update fonts names #101

Version 0.3.0 *(2017-11-8)*
----------------------------

 * New: Gradle plugin updated to 3.0.0 #97
 * New: Add new `fonts` module with Yandex Sans fonts #98

Version 0.2.2 *(2017-09-12)*
----------------------------

 * New: Gradle plugin updated to 2.3.2 #92
 * New: Styles renamed according to library prefix #90
 * New: Gradle wrapper updated to 4.1 #94
 * New: Build tools updated to 26.0.1 #95

Version 0.2.1 *(2015-11-03)*
----------------------------

 * Fix: Updated default style for input fields #83
 * New: Added material text selection handles for Android 4.4 and below #83
 * New: Added style for TextInputLayout: `YaTheme.TextInputLayout` #83
 * New: Added style for button with main action: `YaTheme.Button.MainAction` #86

Version 0.2.0 *(2015-07-18)*
----------------------------

 * Fix: Removed shadow and fixed background for old style action bar (when you don't use `setSupportActionBar`) #79
 * New: Basic initial docs (see README.md) #80

Version 0.1.9 *(2015-06-28)*
----------------------------

 * New: Added styles `YaTheme.Yellow.NoActionBar.FitsSystemWindows` and `YaTheme.White.NoActionBar.FitsSystemWindows`. Use it for layouts with its own status bar representation (e.g., `DrawerLayout`, `CoordinatorLayout`) #73
 * Fix: Changed `YaTheme.Yellow.NoActionBar` and `YaTheme.White.NoActionBar` styles. Use it for layouts with system status bar (e.g., About screen layout), though you might want to add `windowActionBar`/`windowNoTitle` to the base theme instead #73

Version 0.1.8 *(2015-06-21)*
----------------------------

 * New: Released styles module! ('com.yandex.android.uikit:styles:0.1.8') #68 #69

Version 0.1.7 *(2015-06-19)*
----------------------------

 * Fix: Accidental release from dev #64

Version 0.1.6 *(2015-06-19)*
----------------------------

 * New: Gradle plugin updated to 2.1.2 #60
 * New: Support* dependencies updated to 23.4.0 #61

Version 0.1.5 *(2015-03-31)*
----------------------------

 * New: Added 1dp divider to white toolbar #47
 * New: Added `android:textColorHighlight` via new `ya_colors_text_highlight` #51


Version 0.1.4 *(2015-03-22)*
----------------------------

 * New: Added `android:textColorHint` implementation via new `ya_colors_text_hint` #24
 * New: Added `YaTheme.Button.Yellow`, `YaTheme.Button.White` and `YaTheme.Button.Grey` styles #43
 * New: Updated support libraries to 23.2.1 #28
 * Fix: Removed AppBarLayout shadow via zero elevation in style (use `YaTheme.AppBarStyle`) #42
 * Fix: Set `windowActionModeOverlay` to `true` by default #25


Version 0.1.3 *(2015-03-01)*
----------------------------

 * New: Added `android:textColorSecondary` implementation via new `ya_colors_text_secondary`
 * New: Added `android:textColorPrimaryInverse` implementation via existing `ya_colors_text_primary`


Version 0.1.2 *(2015-02-15)*
----------------------------

Initial release.
