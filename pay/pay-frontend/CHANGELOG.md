## 0.83.0 (Fri May 20 2022 10:07:31 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-4121: Update paymentSheetV3 scheme; 98380056
## 0.82.0 (Thu May 19 2022 12:16:30 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-4113: Remove unused code; 163fe3ab
    YANDEXPAY-4112: Fix getting form-url by payment-type; 163bbd6f
    YANDEXPAY-4105: Fix cashback in order-info modal; 29f0b8ac
    YANDEXPAY-4113: Remove CSP checking fetch in sdk; 42bd3105
    YANDEXPAY-4108: Add payment-type to metrika; b6da9fa8
    YANDEXPAY-4112: Update payment-type constants; fb0acdd8
    YANDEXPAY-4001: Split payment objects by payment, payment-token, checkout, checkout-token; 92948e47
[vovanostm]
    YANDEXPAY-4092: added billing_contact to checkout_bolt; 9d08112b
    YANDEXPAY-1784: post message will be sent anyway; 4917d3fc
[kir-9]
    YANDEXPAY-4088: Fix pay by cash on client payment; 3a2a0e3a
    YANDEXPAY-4088: Fix pay by cash on server api; 634e531a
    YANDEXPAY-4000: Update playground for classic bolt; 02336a8e
    YANDEXPAY-4000: Review changes; 7d597890
    YANDEXPAY-4000: Add is_pay_server flag from query; b79ab6f9
    YANDEXPAY-4000: Update client checkout process; 34a708f0
    YANDEXPAY-4000: Add client checkout process; 6377e901
    YANDEXPAY-4000: Add ServerApiModule to checkout; 8b5f15c3
    YANDEXPAY-4002: Update ui classic server api; 9fc149cc
    YANDEXPAY-4000: Payment process in pay-form; d281bb4f
    YANDEXPAY-4000: Payment process as module; c56827c9
## 0.81.0 (Wed May 18 2022 09:00:37 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-4090: Fix tinkoff pay classic header; 2a3974dc
    YANDEXPAY-4087: Fix frame src; 359a082b
    YANDEXPAY-4085: Change check storages logError -> logInfo; 85bc4d88
    YANDEXPAY-4084: Fix fromRedirect param; 18c5aa15
    YANDEXPAY-4073: Fix shipping method PICKUP; 664035ba
    YANDEXPAY-4072: Add currencyCode to pickup option details request; 71ae017c
    YANDEXPAY-4072: Add currencyCode to pickup options request; 5a6ed974
[vovanostm]
    YANDEXPAY-3938: added cashback to checkout; 5061befc
    YANDEXPAY-3989: created switcher for sending receipt for checkout-bolt; 73f4bb2f
## 0.80.0 (Thu May 12 2022 11:43:54 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3890: (checkout, pay-form) Show session-id on error with monospace; ea536802
    YANDEXPAY-3890: (checkout) Remove unused data; 377c5752
    YANDEXPAY-3890: (pay-form) Fix error messages with back buttons; c33e3899
    YANDEXPAY-3890: (checkout) Fix error messages with back buttons; f3953e1a
    YANDEXPAY-4022: (playground) Use mountButton method in classic pay; 388a028a
    YANDEXPAY-4022: (sdk) Add mountButton method; 09da7f60
    YANDEXPAY-3690: (console-registration) Fix content width; fe6ad1b6
    YANDEXPAY-4010: Removed subscription requirement for error and abort; 4288ea41
    YANDEXPAY-4010: Add split errors to booster; 0710c59e
    YANDEXPAY-3970: Work with split with new and current API; 9223dddc
    YANDEXPAY-3876: Update playground icons; 1c151407
    YANDEXPAY-3876: Add border-radius customization; de7ab265
    YANDEXPAY-3876: Use icons instead of text description for custom buttons; 610a6b93
[vovanostm]
    YANDEXPAY-4037: removed dublicated scrollbar, fixed wrap of error message, fixed scroll - focus on top of modal; e0ed67a5
    YANDEXPAY-3690: break-word error info; cab99414
[ruslankunaev]
    YANDEXPAY-3905: iFrame and Storages logs; 047c6ae2
    YANDEXPAY-3890: Show back to store button on critical errors; 26b6d1b5
    YANDEXPAY-3998: Temporary fix 404 icons; b5a4d75c
[skk1020]
    changes; 1ebebe6b
    YANDEXPAY-3876: custom buttons on playground; 6500f90f
    YANDEXPAY-3694: removed step 0 of onboarding for all; c029cdd0
[kir-9]
    YANDEXPAY-3970: Update split status; 90619745
## 0.79.0 (Fri Apr 29 2022 10:54:26 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-4012: Add disabling in webview by Bunker; 4545aee7
    YANDEXPAY-4013: Fix resize button on playground; 520d32e8
    YANDEXPAY-4013: Add cashback exp; 53f7d838
[vovanostm]
    YANDEXPAY-3690: fixed form scroll, error when partner registered twice; 93a15377
## 0.78.0 (Thu Apr 28 2022 07:24:11 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3968: Remove tmp code; ec0d7d0c
    YANDEXPAY-3968: Fix remount Yandex.Pay button; 8f4b97d0
    YANDEXPAY-3968: Set static tuneller host; ea5aec72
    YANDEXPAY-3834: Remove Invalid coupon; 0c738b20
    YANDEXPAY-4004: Rename lable to title for pickup and shipping options; 13daaa39
    YANDEXPAY-3925: Calculate cart options amount for playground; d3308f57
    YANDEXPAY-3999: Add statusText to error log; 8f7d34de
[vovanostm]
    YANDEXPAY-3860: rise up node buffer size to 16kb (like nginx settings, default - 8kb before 14v); 865f1c79
    YANDEXPAY-3860: rise up large buffer size; 086262cd
    YANDEXPAY-3690: fix 500 if api error for encrypt creds; a26d9c0f
    YANDEXPAY-3690: fix styles; 271edcde
    YANDEXPAY-3690: redirect with creds; 8a152004
    YANDEXPAY-3690: fixed offert; 95a17a43
    YANDEXPAY-3690: added callbackUrl for add merch and key value for return in post to cms; 572dc78b
    YANDEXPAY-3690: Bug fix; b48df409
    YANDEXPAY-3690: Error message; 136c0d8c
    YANDEXPAY-3690: Offer for the provision of services; 950479a5
    YANDEXPAY-3690: encrypt creds in registration, show error; 2fb78974
[skk1020]
    YANDEXPAY-3733: warnings when missed important subscribers on Payment; 6914f79b
[kir-9]
    YANDEXPAY-3979: Fix paymentCompleted flag on complete; 9ffd7d34
    YANDEXPAY-3690: Add user logo; 24692d5a
    YANDEXPAY-3690: Update api; 2f615ebd
    YANDEXPAY-3690: Add key for crypto; f8c476c1
    YANDEXPAY-3690: Add service console-registration; 2d3b8ef2
    YANDEXPAY-3690: Add server console-registration; 83d216e4
## 0.77.0 (Fri Apr 22 2022 11:49:32 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3986: Add hide frame control on playground; 9fbde3e0
    YANDEXPAY-3986: Skip split request for unauthorized users; 70a2d6b3
    YANDEXPAY-3986: Fix scaler on new buttons; 75751952
## 0.76.0 (Fri Apr 22 2022 09:48:47 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3983: Fix split button without logo; b013a2b2
## 0.75.0 (Fri Apr 22 2022 09:08:38 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3972: Add custom size control for button; cdc336f5
    YANDEXPAY-3972: Emulate exps on playground; 911dee1e
    YANDEXPAY-3972: Add new button; 76cf0450
    YANDEXPAY-3972: Refactor sdk-payment-method; 804348a3
## 0.74.0 (Wed Apr 20 2022 09:02:41 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-3951: Remove transaction status from success event; ac26fed4
    YANDEXPAY-3951: Add metadata in success event; 42b96c17
    YANDEXPAY-3888: Update styles for touch; 82c083ca
    YANDEXPAY-3940: Add orderAmount without any delivery; 32fba15e
[ruslankunaev]
    YANDEXPAY-3888: Wide button; e03e3de6
    YANDEXPAY-3887: Cash for bolt; dfd532f0
## 0.73.0 (Fri Apr 15 2022 09:37:00 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-3931: Fix javaEnabled flag; 0e1649e2
    YANDEXPAY-3885: Fix checkout button; 7f96cacf
    YANDEXPAY-3885: Fix dragging pay logo; 2267e804
    YANDEXPAY-3930: Fix amount on checkout success modal; bc2d5fb9
    YANDEXPAY-3928: Update pay logo; 687383a3
[vovanostm]
    YANDEXPAY-3885: revert fix for быстро оформить; 61e5144f
    YANDEXPAY-3885: updated old оплатить button icons; 205ea695
    YANDEXPAY-3912: changed pay logo to slide corners on mobile device; 3d2ffeeb
    YANDEXPAY-3885: fix for быстро оформить; 586d30c6
    YANDEXPAY-3885: changed logo in yandex pay button; e0a0b50a
## 0.72.0 (Wed Apr 13 2022 19:55:56 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3924: Remove exps from sdk-init-speedup frame; 449b8db7
    YANDEXPAY-3922: Refactor cart calculation; 73b3cc8e
    YANDEXPAY-3895: Update MKB icon; 14df276b
[kir-9]
    YANDEXPAY-3922: Fix show order items prices; bc3be2bd
## 0.71.0 (Tue Apr 12 2022 15:07:43 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3915: Add metadata to pickup requests; c508de34
    YANDEXPAY-3909: Add billing-contact feature to classic on plaground; 2a891e78
    YANDEXPAY-3796: Fix typo; 96baff2a
    YANDEXPAY-3780: Fix ready-check route; 3bdc9483
    YANDEXPAY-3241: Fix Tinkoff merch-id for dev; 488e6df3
    YANDEXPAY-3873: Remove /public prefix from checkout-api; 3279057e
    YANDEXPAY-3853: Fix metadata for order/create; 1452cb68
    YANDEXPAY-3869: Update playground for checkout.update; c45638b0
    YANDEXPAY-3869: Add update method for checkout; 0776e771
    YANDEXPAY-3858: Fix hiding overlay; 2e8e64cd
    YANDEXPAY-3796: Sync coupons on plaground for checkout and checkout-bolt; 2730862e
    YANDEXPAY-3856: Remove preloader on sync binded card; f1188169
    YANDEXPAY-3794: Rename coupon cart-item on playground; 4514279e
    YANDEXPAY-3854: Remove text from auth-3ds popup; c9e62890
    YANDEXPAY-3853: Fix metadata update on checkout; 72425511
    YANDEXPAY-3846: Prevent emit Abort after Process; 5b814134
    YANDEXPAY-3752: Add CHARGED transaction status; 256e6c74
    YANDEXPAY-3752: Update sdk interface for checkout; 0ae5b110
    YANDEXPAY-3810: Fix env for checkout-sheet; 274051aa
    YANDEXPAY-3810: Fix payment layout on touch; 4cbd62a9
    YANDEXPAY-3810: Update YandexPay button on playground; 5dd936e0
    YANDEXPAY-3810: Add checkout-sheet typing; 7b75f139
    YANDEXPAY-3674: Fixes by review; 6ad5f6a7
    YANDEXPAY-3674: Remove unused code; 37fc7c45
    YANDEXPAY-3674: Update split components; 2bce30fc
    YANDEXPAY-3674: Rewrite payment flow; d9edef68
    YANDEXPAY-3752: Update checkout-sdk on playground; 513e2fd0
    YANDEXPAY-3752: Split sdk payment; 1b886d01
    YANDEXPAY-3534: Update jwt decoder; 891ac307
    YANDEXPAY-3534: Use checkout buttons on playground; bd629ba2
    YANDEXPAY-3534: Skip payment destroy on error; d3bfdecf
    YANDEXPAY-3534: Fix routing on playground; 5f759fb0
    YANDEXPAY-3535: Fix playground build; 7e514e54
    YANDEXPAY-3535: Add reset logs; f7937fe7
    YANDEXPAY-3535: Destroy payments on unmount; 63f75aa7
    YANDEXPAY-3534: Move create order to services; 3bf5435f
    YANDEXPAY-3534: Update create payment; c1d65f0a
    YANDEXPAY-3718: Fix classic button on playground; 9382e6ad
    YANDEXPAY-3718: Add coupons and pickup-options; f0c08036
    YANDEXPAY-3718: Update playground nginx config; c91c0a2a
    YANDEXPAY-3718: Remove checkout-mock from Procfile.checkout; 6e379d02
    YANDEXPAY-3718: Add playground settings on server; 9256e54b
    YANDEXPAY-3718: Add classic pay-button to checkout; af66cb17
    YANDEXPAY-3718: Update playground for bold; 8016ac07
    YANDEXPAY-3718: Add playground-data package; 28464040
    YANDEXPAY-3718: Fix priority of rum messages in console; 4734b6f1
    YANDEXPAY-3718: Fix typings; ccc22ad4
    YANDEXPAY-3718: Update README; 5ac3f782
    YANDEXPAY-3718: Update merch-id for bolt; 3df40322
    YANDEXPAY-3718: Refactor playground; 2f8472f5
    YANDEXPAY-3718: Remove unused code; 5ab62186
    YANDEXPAY-3718: Move playground to bff; 85139017
    YANDEXPAY-3562: Fix checkout-mock urls; 6e15664f
    YANDEXPAY-3535: Fix server typings; a422cef1
    YANDEXPAY-3685: Refactor server checkout; c78cf1cc
    YANDEXPAY-3562: Update checkout-mock for new bolt-api; 95858b09
    YANDEXPAY-3562: Add static upload for checkout-mock; 41b11601
    YANDEXPAY-3562: Rewrite checkout-mock for boltify; 1346390e
    YANDEXPAY-3524: Add meta info to payment sheet; fc4647e8
    YANDEXPAY-3524: Rewrite Sdk typings; 196c3435
    YANDEXPAY-3524: Add sdk.createCheckout method; dfebbf52
[kir-9]
    YANDEXPAY-3528: Add rum delta transaction; a7e30e29
    YANDEXPAY-3528: Add server checkout counters; e3160645
    YANDEXPAY-3241: Add new merchant kir-9; f6246367
    YANDEXPAY-3874: Add csp rule for sandbox; 0e0d7b84
    YANDEXPAY-3685: Update order create; c36d6f93
    YANDEXPAY-3525: Update payment-method: PaymentSheet -> InitPaymentSheet; cf411438
    YANDEXPAY-3659: Add checkout module in store; a6e903ab
    YANDEXPAY-3659: Checkout as feature; 9675aaea
    YANDEXPAY-3530: Update order api; 8f090c9f
    YANDEXPAY-3530: Rename new api order -> checkout server api; 2bdd2ca9
    YANDEXPAY-3620: Add mock for existing api methods; d53994c6
    YANDEXPAY-3620: Add mock; fdf696f4
    YANDEXPAY-3530: Add new order api module like rpc; 6b30fdda
    YANDEXPAY-3529: Update new api order schema; e6b8a7d3
    YANDEXPAY-3529: Add new api data transforms; 000907fd
    YANDEXPAY-3529: Add requests to new order api; 22d70b63
[ruslankunaev]
    YANDEXPAY-3795: Fix merchant in playground; fcc7ca2a
    YANDEXPAY-3676: Boltify Threeds; b92733b1
    YANDEXPAY-3675: Add payment logic; 3e23c752
    YANDEXPAY-3535: Remove console.log and add memoize; c4afcf2d
    YANDEXPAY-3535: Rebase and add mock opener; 92b485fa
    YANDEXPAY-3535: Fix review comments; 4160796c
    YANDEXPAY-3535: Add logic work with server in playground; e2d435fd
    YANDEXPAY-3535: Modify playground; 4f9a2196
[skk1020]
    YANDEXPAY-3729: reset button moved to playground; 6766d5c2
## 0.70.0 (Mon Apr 11 2022 13:47:27 GMT+0000 (Coordinated Universal Time))

[vovanostm]
    YANDEXPAY-3857: added rum counter to check difference of speedup and base init; f6b8a30b
    YANDEXPAY-3776: set theme settings for some merchants; 60e50a8e
[ruslankunaev]
    YANDEXPAY-3845: Copy icons with frozen names to frozen SDK; 1be06d39
    YANDEXPAY-3844: Remove RUM from init-frame (speedup); f5f1f791
[kir-9]
    YANDEXPAY-3811: Add bunker to sdk-payment-method service; 4eca269b
    YANDEXPAY-3790: Add new currencies; 8341e58c
## 0.69.0 (Tue Apr 05 2022 07:36:02 GMT+0000 (Coordinated Universal Time))

[ruslankunaev]
    YANDEXPAY-3743: Check robokassa errors; 2115a1e0
    YANDEXPAY-3755: Fix card disappearing on window resize; 3bb18d01
    YANDEXPAY-2289: Fix close window logs; 30150544
## 0.68.0 (Mon Apr 04 2022 13:57:41 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3830: Add route old url-scheme for init-speedup; 12f605dc
## 0.67.0 (Fri Apr 01 2022 10:42:41 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3800: Restore changelog; 9f70c048
    YANDEXPAY-3808: Remove demo pages from docker; e99ca777
    YANDEXPAY-3800: Fix icon logo; a2b2b52b
    YANDEXPAY-3800: Update logo on classic checkout; 47851db6
## 0.66.0 (Mon Mar 28 2022 10:55:47 GMT+0000 (Coordinated Universal Time))

[axb48]
    YANDEXPAY-3701: Added build_version to ya_metric and rum log; 226f6b76
    YANDEXPAY-3680: рефактор; deccf5df
    YANDEXPAY-3680: отрефакторил на новую проверку по таймеру; 6b8e69fb
    YANDEXPAY-3680: добавил iframe только с данными из бункера, добавил таймер для анализа скорости инициализации iframe; ce8efc41
[kir-9]
    YANDEXPAY-2405: Sdk pay button as preloader for checkout; 63d543e5
[skk1020]
    YANDEXPAY-2969: added sessionId too error screens; 7c3f05fd
    YANDEXPAY-2512: add normalization in geo saggest; 8f535e2f
## 0.65.0 (Tue Mar 15 2022 09:28:10 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3484: Fix Promise sdk; 0a3e3203
    YANDEXPAY-3340: Add env param for ready-to-pay-check; 710051be
    YANDEXPAY-2079: Update log form loading; 60745c4b
    YANDEXPAY-3484: Remove unused code; ada9cd36
    YANDEXPAY-3484: Refactor lib/is; 538b423b
    YANDEXPAY-3484: Fix send updates with void; 40980a88
[sudilovskiy]
    YANDEXPAY-1612: Extend few JSDocs; 0b2957fb
    YANDEXPAY-1612: Extend 'HtmlToolsTagsGenerator' JSDoc; da671543
    YANDEXPAY-1612: Extend 'HtmlToolsTagsGenerator' JSDoc; f68fcba8
[ruslankunaev]
    YANDEXPAY-3484: Add Promise support for SDK; d2c3a654
[kir-9]
    YANDEXPAY-2079: TEMP playground test race condition; fa8a6f4c
    YANDEXPAY-2079: Log update on not ready form; b88f5ef8
## 0.64.0 (Wed Mar 09 2022 06:43:15 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3353: Move checkout under /web prefix; c3fab02b
    YANDEXPAY-3353: Add /web prefix to nginx configs; 1df17088
    YANDEXPAY-3353: Move services under /web prefix; ca6e5afc
    YANDEXPAY-3353: Add rewrites to services config; 0884fc7d
    YANDEXPAY-3353: Simplify SDK config; e362fe71
    YANDEXPAY-3499: Move favicons to S3; efa01320
## 0.63.0 (Sat Mar 05 2022 10:23:45 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-2763: Update userLocation -> user.location; 6d684b38
    YANDEXPAY-2763: Add button for location to yandex maps; 84269e66
    YANDEXPAY-2763: Add user location by ip; 2cd10957
## 0.62.0 (Sat Mar 05 2022 06:53:28 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3650: Rename mobile-api-assets icons; da4cde11
## 0.61.0 (Wed Mar 02 2022 08:28:38 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3626: Update caniuse-lite; 76e5e8d9
    YANDEXPAY-3624: Fix playground html; 95a12ead
    YANDEXPAY-3499: Fix Bunker config; 7e031a8e
## 0.60.0 (Tue Mar 01 2022 12:47:41 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3622: Add Access-Control headers; e2e31bf3
## 0.59.0 (Mon Feb 28 2022 11:17:32 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3519: Rename bunker middleware; d74d41ce
    YANDEXPAY-3499: Remove nginx locations for services with S3 static; 7fcf864b
    YANDEXPAY-3499: Add S3 upload for mobile-api-assets; 85c214d0
    YANDEXPAY-3499: Update yastatic CSP; ae253026
    YANDEXPAY-3499: Update Dockerfile; 2fa9a993
    YANDEXPAY-3499: Update s3 paths for different releases; 0ad9ff12
    YANDEXPAY-3499: Update global favicon; 24e95dcb
    YANDEXPAY-3499: Fix mobile-api-assets hrefs; 05a5b2d3
    YANDEXPAY-3499: Refactor services config; 75cdfb87
    YANDEXPAY-3499: Move favicons to S3; c97779ce
    YANDEXPAY-3519: Update bunker interface; 4d04aa0c
    YANDEXPAY-3499: Update webpack configs; 1f5bb790
    YANDEXPAY-3499: Update svg plugin; 552f1c82
    YANDEXPAY-3499: Move secondary services to separete Procfile; 10161fc6
    YANDEXPAY-3499: Webpack@5.69.0; 6223999e
    YANDEXPAY-3499: Add static upload to S3; 5e497469
    YANDEXPAY-3499: Add @yandex-int/static-uploader; c3d404ec
    YANDEXPAY-3499: Rename service config folder to .config; 8b0898fa
[ruslankunaev]
    YANDEXPAY-3519: Add bunker to project; 836b2329
## 0.58.0 (Fri Feb 25 2022 09:49:21 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3590: Fix resetting coupons; 1e6be920
    YANDEXPAY-3592: Fix playground on multiple sessions; abc709ae
## 0.57.0 (Thu Feb 24 2022 09:23:55 GMT+0000 (Coordinated Universal Time))

[ruslankunaev]
    YANDEXPAY-3380: Fix border-radius bug and show promocode activated after refresh; 48bfe841
    YANDEXPAY-2767: Request more info about selected pickpoint; 1f6f3039
    YANDEXPAY-3472: Check CSP and measure time between SDK init and create payment; 3f621bb3
[stepler]
    YANDEXPAY-2767: Update pickup point title; e7f4ea79
    YANDEXPAY-2767: Update pickup request typings; 91fde9da
    YANDEXPAY-2767: Update playground; 468b8653
    YANDEXPAY-3380: Add 50% test coupon; ce0bb3b4
[kir-9]
    YANDEXPAY-3380: Update styles; 63851bf5
    YANDEXPAY-3380: Update setErrorWithPingOpener; 27be03e0
    YANDEXPAY-3380: Add coupon counters; 610c6e16
    YANDEXPAY-3380: Update acceptCoupons -> coupons; 764b8ba7
    YANDEXPAY-3380: Add coupon reset to playground; a38063b4
    YANDEXPAY-3380: Add coupon success; b11dc9d5
    YANDEXPAY-3380: Add coupon view page; a0fd4158
    YANDEXPAY-3380: Add coupon widget; 585880ae
## 0.56.0 (Tue Feb 22 2022 12:16:31 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3574: Update split button view without avatar; 30e2e87d
    YANDEXPAY-3579: Fix sdk timers; 46b7bca3
[kir-9]
    YANDEXPAY-3578: Update split button counter; 23667638
    YANDEXPAY-3574: Add split text without avatar; 80b90824
## 0.55.0 (Fri Feb 18 2022 14:58:00 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3565: Update split_toggle event; 30c6439a
    YANDEXPAY-3565: Add split_available event on touch; af44f546
## 0.54.0 (Fri Feb 18 2022 08:42:27 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3544: Remove users whitelist for Split; 4c6f4ca9
## 0.53.0 (Wed Feb 16 2022 14:08:30 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3521: Remove send counters delay from split checkout; 708a23f9
[ruslankunaev]
    YANDEXPAY-3521: Add pending screen on split payment and add marchart; 54d90b2d
## 0.52.0 (Tue Feb 15 2022 15:59:04 GMT+0000 (Coordinated Universal Time))

[ruslankunaev]
    YANDEXPAY-3515: Fix CSP for split; 6c95312f
    YANDEXPAY-3508: Remove staff access to split; 6549aa80
    YANDEXPAY-3507: Log active time for split frame; 6a70c39b
## 0.51.0 (Tue Feb 15 2022 11:44:30 GMT+0000 (Coordinated Universal Time))

[ruslankunaev]
    YANDEXPAY-3465: Add no fee text to split; 02658ef7
    YANDEXPAY-3447: Fix scroll in cart; deb33900
    YANDEXPAY-3478: Reformat cashback word; 2239f945
    YANDEXPAY-3458: Add secure icon when split enabled; 70936e25
[stepler]
    YANDEXPAY-3497: Fix Split success window width; 1624081a
    YANDEXPAY-3447: Remove scroll from split success screen; 7891b6d9
    YANDEXPAY-3448: Fix months formatter; c4ef62ef
    YANDEXPAY-3341: Increase Split window size; 5c9f56e8
    YANDEXPAY-3225: Add selecting binded card; 3930676b
    YANDEXPAY-3225: Fix binding-form disabled button; 06184748
    YANDEXPAY-3225: Restore Split for test; 394e39da
[polrk]
    YANDEXPAY-3225: Create binding form; 3d6b5fc1
    YANDEXPAY-3225: Fix split available metrik; 2d4cea30
    YANDEXPAY-3225: Add metriks; e04d9ee1
    YANDEXPAY-3225: Remove console.log; e57e5f22
    YANDEXPAY-3225: Update step messages; 786b6cdc
    YANDEXPAY-3225: Add card gen file; e4fc0872
    YANDEXPAY-3225: Fix frame updates; bfb2910e
    YANDEXPAY-3225: Update stiles; b7114ca2
    YANDEXPAY-3225: Feat add split payment form; c9a1ad9d
    YANDEXPAY-3225: Feat add universal Payment Form; 1c0372bc
## 0.50.0 (Thu Feb 10 2022 12:28:23 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3457: Fix detect Android webview; 4ca75052
    YANDEXPAY-3193: Fix user uid getter; c361589e
    YANDEXPAY-3193: Add CSP rule for sandbox split frame; ad890e0f
    YANDEXPAY-3193: Add ivaxer uid in split whitelist; 75b5e70e
    YANDEXPAY-3193: Add BSH uids in split whitelist; 40c51ffd
    YANDEXPAY-3444: Call /api/v1/user_cards on new card only; 400c5054
## 0.49.0 (Fri Feb 04 2022 16:33:57 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3424: Fix getting avatar on pay-form; ab9b2d70
[kir-9]
    YANDEXPAY-3422: Fix touch counters; 88bcde9e
## 0.48.0 (Thu Feb 03 2022 14:56:10 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-3212: Fix table width; 5cf86f83
## 0.47.0 (Thu Feb 03 2022 11:54:33 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3393: Fix connection for native target; 1b77c3e2
    YANDEXPAY-3321: Add checkout intercom for mobile native; 5e216224
    YANDEXPAY-3342: Fix /web-api/mobile/v1/user_info; 942d6706
[kir-9]
    YANDEXPAY-3394: Fix routes counters; ff661754
    YANDEXPAY-3212: Add max height to cart items block; 3691b2e9
    YANDEXPAY-3202: Update check iframe; 7e0b888f
    YANDEXPAY-3224: Add scaler for cashback; aa80a264
[polrk]
    YANDEXPAY-3224: Make scaler a singleton; 9db0d384
    YANDEXPAY-3224: Remove debug code; cfd11312
    YANDEXPAY-3224: Add scaler for block component; 760a9e85
    YANDEXPAY-3224: Remove String(); 9dca336e
    YANDEXPAY-3224: Use css function; 67f452e4
    YANDEXPAY-3224: Replace unsupported zoom; 8a4ea4c1
    YANDEXPAY-3195: Update split selector; 4cd032f8
    YANDEXPAY-3197: Update split faq; d18803b1
    YANDEXPAY-3195: Skip sync user card for cash; 263e795a
## 0.46.0 (Fri Jan 28 2022 09:03:52 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3234: Fix server build; 81311c6c
    YANDEXPAY-3234: Remove monochrome logo; 894a4756
    YANDEXPAY-2877: Add success Split payment message; d670941f
    YANDEXPAY-2877: Add random order-id; bed5daf4
    YANDEXPAY-2904: Add Split frame; fa099b2f
    YANDEXPAY-2877: Refactor routes; 777669f3
    YANDEXPAY-2877: Remove unused code; 84f12adb
    YANDEXPAY-2967: Add split for users with phone; 38447ae5
    YANDEXPAY-2905: Add Split pay button; 12f60195
    YANDEXPAY-2880: Move Split store to own branch; cbec4795
    YANDEXPAY-2880: Add Split plan on main screen; dcda6e9f
    YANDEXPAY-2880: Add Tumpler component; 7282f444
    YANDEXPAY-2967: Add info about users phone; fa2fc9b3
    YANDEXPAY-3202: Update webview checks; 440a57f6
    YANDEXPAY-1487: YandexPay Button avatar-border for white themes; c5fb051f
    YANDEXPAY-3036: Add sync for new binded cards; 183a4693
[ruslankunaev]
    YANDEXPAY-3175: Expand widgets on desktop and increase license font-size; 46ef3521
    YANDEXPAY-3235: Add plus popup in cart; 5670de4b
    YANDEXPAY-3250: Add shipping option and pickup point id to checkout; d8e593e7
    YANDEXPAY-3197: Add popups for split and plus; 640a08d3
    YANDEXPAY-3195: Handle cash payment method for split; 37189def
    YANDEXPAY-3053: Add split success screen; e6a7fbf8
[kir-9]
    YANDEXPAY-3222: Stay checkout window opened with split; 9a916125
    YANDEXPAY-3198: Split check on payment update; ea76a1e0
    YANDEXPAY-3198: Check available split from backend; a56e8866
    YANDEXPAY-3227: Add split available with whitelist; e373b780
    YANDEXPAY-3198: Fix split available; 103d9ccb
    YANDEXPAY-3054: Add split errors; 896c8054
    YANDEXPAY-2877: Add split to playground; 317300fc
    YANDEXPAY-3202: Add check webview with frame to sdk-ready-check; 803ea8e7
    YANDEXPAY-3202: Not show button in webview + iframe; ecc66433
[polrk]
    YANDEXPAY-3234: Add monochrome logo for brandshop; 7cdb3839
    YANDEXPAY-2907: Remove other merchant ids for split on testing; acb629a8
    YANDEXPAY-2907: Remove other merchant ids for split; 91c1b573
    YANDEXPAY-2907: Extract method; ad9d9c3e
    YANDEXPAY-2907: Add split textline to button; 04938056
    YANDEXPAY-2907: Add split config; f20ce37f
    YANDEXPAY-3036: Update run configurations; 5a142c20
## 0.45.0 (Thu Jan 27 2022 10:16:39 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3318: Remove console sid for metrika; d9504b33
    YANDEXPAY-3318: Fix crash console page; ae3aca2a
## 0.44.0 (Wed Jan 26 2022 12:34:05 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-3291: Remove debug code; f34f6dff
    YANDEXPAY-3291: Add email validation to console onboarding; 3a1eaa47
    YANDEXPAY-3272: Add oauth for blackbox; dc5b3b6b
[kir-9]
    YANDEXPAY-3285: Add console counter id; e8acd089
    YANDEXPAY-3145: Update addresses counters; 8eb58060
    YANDEXPAY-3245: Update console agreement; c5c13e4b
[polrk]
    YANDEXPAY-3145: Extract transformation logic; c5d242fd
    YANDEXPAY-3245: Add default values; 7541ac5f
    YANDEXPAY-3245: Add counter; f664d65b
    YANDEXPAY-3245: Show Email only if email doesnot exists; d75a1f96
    YANDEXPAY-3245: Add input component; 6069a869
    YANDEXPAY-3245: Update express blackbox dependency; 17cee337
    YANDEXPAY-3145: Send counter before sending form; bcd7c749
    YANDEXPAY-3145: Add new counter; 5727c6e3
    YANDEXPAY-3145: Send address part existing; 3fbd2cf7
    YANDEXPAY-3145: Add analytics wrapper; 309a2f5a
    YANDEXPAY-3145: Add ids; 09c33b29
    YANDEXPAY-3145: Add addresses metriks; 9f6594ef
## 0.43.0 (Wed Jan 19 2022 11:07:27 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-3079: Update agreement text; b8dc7429
    YANDEXPAY-3079: Fix ios layout; c2e33d7f
    YANDEXPAY-3079: Add console csp; d194a716
    YANDEXPAY-3079: Remove unnecessary code; 4bc26494
    YANDEXPAY-3079: Add offerAccepted param; 62d63425
    YANDEXPAY-3079: Update console template; c3c942f5
    YANDEXPAY-3079: Update nginx config for console; cbc0d711
    YANDEXPAY-3079: Add console api links; 59c59fff
    YANDEXPAY-3079: Add local request to test backend; 87edde89
    YANDEXPAY-3079: Get merchant data and push to parent window; f91e346f
    YANDEXPAY-3079: Add agreement text; ba2617d5
    YANDEXPAY-3079: Add agreement page; ddf0a026
    YANDEXPAY-3079: Add checkbox component; 33c3de1e
    YANDEXPAY-3079: Add service console; ef0b7a9f
## 0.42.0 (Thu Jan 13 2022 13:13:43 GMT+0000 (Coordinated Universal Time))

[ruslankunaev]
    YANDEXPAY-3169: Fix currency symbols and remove BYR; f527aff3
    YANDEXPAY-3148: Add new currencies; 0f3d5d2f
## 0.41.0 (Tue Jan 11 2022 14:47:42 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-3158: Add ob info on first step; efad1d94
    YANDEXPAY-3143: Set onboarded flag with exp; 3a5737c0
    YANDEXPAY-3143: Add exp checkout_without_onboarding; f0fbdf68
## 0.40.0 (Mon Dec 27 2021 10:29:24 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2877: Fix static for test; b7d1a76b
    YANDEXPAY-2682: Add full light icons; 9583e5e5
    YANDEXPAY-2682: Add service to Docker; b4072d51
    YANDEXPAY-2682: Add mobile-api-assets-v2; f98052a7
    YANDEXPAY-2682: Add combine util; b6f10ec4
[kir-9]
    YANDEXPAY-3038: Fix button title; 8e4df3b2
## 0.39.0 (Thu Dec 23 2021 17:00:10 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-3080: Fix cart in header; a70f8b89
## 0.38.0 (Wed Dec 22 2021 11:43:30 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2898: Restore merch ids for test; ab482254
    YANDEXPAY-3011: Add exp with Yellow btn; baf633ee
    YANDEXPAY-2848: Update yellow theme colors; 5bfd3019
    YANDEXPAY-2848: Update merch-ids; 14c106d6
    YANDEXPAY-2847: Update error messages and validation regexp; d9ed13cd
[kir-9]
    YANDEXPAY-2848: Disable personalize on back; 03a604e7
    YANDEXPAY-2848: Add button for bills; 4d14f363
    YANDEXPAY-2848: Add yellow theme; 94e73ec0
    YANDEXPAY-2847: Update input hint style; 9639a1e1
    YANDEXPAY-2847: Get user name from passport; 5629bf13
    YANDEXPAY-2847: Add billing contact name to playground; 52418dd3
    YANDEXPAY-2847: Add name to pay-form; b6c7cfbe
    YANDEXPAY-2906: Update link to agreement cashback view; f2a791b4
    YANDEXPAY-2906: Update cashback view in pay-form; 4b5210a8
    YANDEXPAY-2906: Add cart to pay-form; 6527ca4a
## 0.37.0 (Fri Dec 17 2021 15:22:23 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2988: Fix log additional data; d1b9f542
## 0.36.0 (Fri Dec 17 2021 13:43:36 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2988: Add contacts logger; 03c8e69c
## 0.35.0 (Mon Dec 13 2021 10:38:06 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-2909: Add map behaviors on map reset; 0d79c9bc
[stepler]
    YANDEXPAY-2274: Remove sourceUrl from message in query connection; 556884a9
    YANDEXPAY-2274: Fix tests; 352122bf
    YANDEXPAY-2274: Remove __YP__ from sourceUrl in query connection; ea8fbb94
## 0.34.0 (Wed Dec 08 2021 12:59:38 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2749: Add global listiner for pickpoints; 900a92a6
    YANDEXPAY-2749: Update queue rpc; 7f424c7c
    YANDEXPAY-2749: Add collecting points; 1b8b4c31
[kir-9]
    YANDEXPAY-2749: Add queue rpc; 11d25b42
    YANDEXPAY-2749: Fix pickup points on error; 327000a3
    YANDEXPAY-2749: Await all pickup points listeners; d97bed4b
    YANDEXPAY-2749: Add only new points on map; a94095d8
    YANDEXPAY-2822: Change timeout fetch points; 2b2c1e22
## 0.33.0 (Mon Dec 06 2021 15:52:01 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-2819: Add updated cookie event; 4a98cfa4
    YANDEXPAY-2819: Add update cookie counter; b1352cfc
    YANDEXPAY-2819: Fix blackbox url; 05167f55
    YANDEXPAY-2819: Add reset session route; 390d576f
    YANDEXPAY-2819: Redirect to passport update on NEED_RESET; 71f1868b
## 0.32.0 (Wed Dec 01 2021 09:36:55 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-2770: Load points on bounds area; b245cf81
    YANDEXPAY-2596: Fix set map margin; c7c3f689
## 0.31.0 (Tue Nov 30 2021 10:55:20 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2770: Fix pickpoint cache; ecbe3470
    YANDEXPAY-2770: Fix async data typings; 0f1ccf0d
    YANDEXPAY-2770: Disable pickpoint cache; 6e6073e8
## 0.30.0 (Mon Nov 29 2021 12:20:57 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2760: Fix logger in sdk; 97ff6fde
    YANDEXPAY-2487: Add user to FF; 7ab29ca9
    YANDEXPAY-2756: Fix rpc race-condition; 309530a0
    YANDEXPAY-2750: Update initial map zoom; 5a17a059
    YANDEXPAY-2560: Fix map cache on 15+ zoom; 41170b99
    YANDEXPAY-2560: Add TODO; d8d9bc68
    YANDEXPAY-2560: Fix initial zoom; 3635b2c3
    YANDEXPAY-2717: Add zoom by suggest type; e14542b6
    YANDEXPAY-2560: Fix after rebase; e57f35f0
    YANDEXPAY-2560: Add pickpoint cache; 4c9d5737
    YANDEXPAY-2560: Fix bounds coords parser; 2e1c9aad
    YANDEXPAY-2560: Add geo lib; 50e3fe3a
    YANDEXPAY-2540: Fix pickup without setup points; ca4d8f77
    YANDEXPAY-2540: Add calc center of setup points; 74a76cae
    YANDEXPAY-2540: Fix and refactor Map; 121a67ab
[kir-9]
    YANDEXPAY-2762: Request to order on every shipping change; 62db7799
    YANDEXPAY-2754: Redirect to ob start route on initial; efc1b53e
    YANDEXPAY-2752: Fix show choose shipping type component; 715e4b15
    YANDEXPAY-2751: Fix no-placemarks-popup; c7b2abd8
    YANDEXPAY-2739: Add check current shipping type at cart; 0b0e4685
    YANDEXPAY-2723: Fix pickup date info; e6977ac5
    YANDEXPAY-2721: Create circle of points with same coords; 82698483
    YANDEXPAY-2601: Fix touch map layout; 93501e6b
    YANDEXPAY-2670: Add shipping info to checkout api; eab15404
    YANDEXPAY-2649: Add rum logs; 521f7042
    YANDEXPAY-2649: Add pickup counters; 0a963486
## 0.29.0 (Wed Nov 24 2021 12:35:10 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2709: Remove checkout mock; 29c32798
    YANDEXPAY-2540: Add setup event; 6f886593
    YANDEXPAY-2654: Restove api2 for sandbox; e36a1703
    YANDEXPAY-2589: Fix getMerchant fn; a67b2ac0
    YANDEXPAY-2589: Update mock order items; 1706ca80
    YANDEXPAY-2589: Refactor selectors; aba5a952
    YANDEXPAY-2589: Emulate merchants cart; dfcef3e5
    YANDEXPAY-2655: Fix playground option iterator; 598fc59e
    YANDEXPAY-2607: Restore mock; 3f2a4862
    YANDEXPAY-2607: Add setup payment method; 184afd69
    YANDEXPAY-2607: Update PickupPoint fields; 36e4d0dc
    YANDEXPAY-2551: Update pickpoints mock; 7484ee2d
    YANDEXPAY-2561: Add challenge to cart variant; 3f06908a
    YANDEXPAY-2561: Add verification challenge on checkout form; fbd32181
    YANDEXPAY-2561: Remove FF flags for checkout challenge; c0349f8a
[kir-9]
    YANDEXPAY-2696: Add region to address; 8ed0d25b
    YANDEXPAY-2677: Fix search address on pickup; e3040d7c
    YANDEXPAY-2643: Fix zoom on initial bounds; ac23e96e
    YANDEXPAY-2643: Add map bounds by placemarks; 343ea82c
    YANDEXPAY-2653: Add holodilnik logo; acfb4fb9
    YANDEXPAY-2650: Add max map zoom; b526f8d0
    YANDEXPAY-2641: Add no-placemarks popup on update error; 37b40d2b
    YANDEXPAY-2645: Fix pickup info margin; 23f944f8
    YANDEXPAY-2640: Fix OB on add address; 99ca942d
    YANDEXPAY-2590: Show no-placemarks only on pickup page; b733e483
    YANDEXPAY-2487: Fix tabs shipping; 4e75399d
    YANDEXPAY-2452: Add pickup onboarding; 64d3b75f
    YANDEXPAY-2591: Fix error on setup pickup; 62543482
    YANDEXPAY-2604: Fix drawer search z-index; 0f1a8af1
    YANDEXPAY-2445: Fix styles; dc4f82b9
    YANDEXPAY-2547: Add popup no placemarks; d21494b8
    YANDEXPAY-2507: Add touch pickup address select; 11489a54
    YANDEXPAY-2530: Show map by all placemarks once; 1f1d47b1
    YANDEXPAY-2493: Add tabs for choose shipping type; 096447c8
    YANDEXPAY-2448: Optimize pickup; 48ec5d23
    YANDEXPAY-2448: Update pickup pages; 55e09ebe
    YANDEXPAY-2448: Add initial points; 557ff1a7
    YANDEXPAY-2448: Add pickup map; 6a5d2e08
    YANDEXPAY-2447: Add pickup points mock; 729aa0b6
    YANDEXPAY-2446: Add select shipping type; 88d10e3d
[ruslankunaev]
    YANDEXPAY-2525: Add shipping time slots; e392a3a6
    YANDEXPAY-2525: Add shipping time slots; 6493e4ab
    YANDEXPAY-2550: Custom cluster icon; 32d97bdb
    YANDEXPAY-2554: Add select pickup point logic; 0990ccb8
    YANDEXPAY-2545: Change pin icon to touch version in pickup selected page; 2545d86e
    YANDEXPAY-2538: Remove tabs when pickup unavailable; 802981be
    YANDEXPAY-2486: Add work with rpc in pickup store; 094cf8f0
    YANDEXPAY-2528: Move pickup setup to app initialization; 28747c13
    YANDEXPAY-2451: Add pickup to main screen; d3b4dc1e
    YANDEXPAY-2450: Add selected pickup point info screen; b8130098
[polrk]
    YANDEXPAY-2589: Add delivery kind in title; 7dcef089
    YANDEXPAY-2549: Rename class name; 36cbe912
    YANDEXPAY-2549: Add pickup loader; 55322459
    YANDEXPAY-2602: Reset order after complete; ffa56a92
    YANDEXPAY-2591: Add map state presets; b88a1b27
    YANDEXPAY-2591: Update code style; 4318b73c
    YANDEXPAY-2670: Remove double map showing logic; 4d2c5afe
    YANDEXPAY-2670: Remove console.log; 99075e6f
    YANDEXPAY-2670: Use map from redux; 40ebad93
    YANDEXPAY-2670: Use map presets; e1bd4fa3
    YANDEXPAY-2670: Use enum for map layout variants; 4f1bde39
    YANDEXPAY-2670: Add conventers; af56b852
    YANDEXPAY-2670: Add map preset hook; 70cca402
    YANDEXPAY-2670: Do not remove old pickup points; 77c4b734
    YANDEXPAY-2670: Add map state; 19a6942d
    YANDEXPAY-2670: Update redux logger config; af1da0be
    YANDEXPAY-2670: Use async from util package; 87b33b92
    YANDEXPAY-2670: Update app config; 8b5d34d1
    YANDEXPAY-2670: Remove unused import; 319f8fad
    YANDEXPAY-2670: Add Async typigns; f32265c6
    YANDEXPAY-2670: Add Yandex maps typings; e54a3fb2
    YANDEXPAY-2670: Use map api key in client services; 75c0fcc0
    YANDEXPAY-2670: Update async util; 17284da7
    YANDEXPAY-2670: Send only map api key; dc92e7f1
    YANDEXPAY-2670: Add types support for contain fn; 74a17bc0
    YANDEXPAY-2670: Add produce into services; 36ef7ef5
    YANDEXPAY-2454: Add proxy to run scripts; 27a93ba6
    YANDEXPAY-2454: Update proxy server; da18a08a
    YANDEXPAY-2454: Update checkout; da25b27b
    YANDEXPAY-2454: Update favicon; e6d546c5
    YANDEXPAY-2454: Add pickup section; 621d2e1f
    YANDEXPAY-2454: Update sdk typings; 2c2d310a
## 0.28.0 (Fri Nov 12 2021 15:27:21 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2510: Add agent info to meta; 5f54e5d2
    YANDEXPAY-2413: Fix load cashback in payment method; 27eb79b4
    YANDEXPAY-2403: Fix collect extra data; 5e7a675f
    YANDEXPAY-2535: Fix passport challenge for testing; 51f61a36
    YANDEXPAY-1911: Add log for DeprecatedButton usage; 16c60e29
    YANDEXPAY-1911: Restore ErrorEventReason type; 0a7117d3
    YANDEXPAY-2403: Move fake response decorator to request logic; bc10feb0
    YANDEXPAY-2351: Add tests for page-focus-watcher; 64680fe9
    YANDEXPAY-2351: Add visible state to warn-log; 78345ef6
    YANDEXPAY-2351: Apply exp 'immediate-close-form'; 1c0b489d
    YANDEXPAY-2491: Add order amount value to process event; f42f0182
[sudilovskiy]
    YANDEXPAY-1911: Add warning text; 7784faf8
    YANDEXPAY-1911: Add logger of method usage; 73b0e503
    YANDEXPAY-1911: Remove method name from deprecation warning; 628d1b82
    YANDEXPAY-1911: Add 'try..catch'; 18be4efb
    YANDEXPAY-1911: Replace 'ErrorEventReason' enum with mock; 8b676969
    YANDEXPAY-1911: Bump TS 'lib' version to work with 'Symbol'; be4ee263
    YANDEXPAY-2403: Add fake Response handling by 'errorByStatus' decorator; e2b74c64
    YANDEXPAY-2403: Add tests for error name formatting; 0e6da3b5
    YANDEXPAY-2403: Remove 'statusText' wrap; 1a7620f8
    YANDEXPAY-2403: Extract 'getMissingErrorName'; 38689292
    YANDEXPAY-2403: Preserve original error name and description; fd5db84b
    YANDEXPAY-2403: Update links and project name; 8d898a8e
    YANDEXPAY-2403: Add version to tracker data; c5db7aaa
    YANDEXPAY-2403: Concatenate constructor name to error message; 7c5327b0
    YANDEXPAY-2403: Remove redundant 'message'; f177bf04
    YANDEXPAY-2403: Add try..catch decorator; e8b9c452
    YANDEXPAY-2403: Remove instance check; c7678b5d
    YANDEXPAY-2403: Move method to constructor; 1a623a35
    YANDEXPAY-2403: Add method and request id to 'FetchHttpError'; e4fda175
    YANDEXPAY-2403: Add 'toJSON' support for obtaining extar dat from errors; 39079ca6
[polrk]
    YANDEXPAY-2454: Update cashback after coupon apply; 2fef6faa
## 0.27.0 (Wed Nov 10 2021 11:16:26 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2508: Add verification challenge on playground; 4f8a620b
    YANDEXPAY-2508: Enable verification challenge by payment-sheet; eb8d7543
    YANDEXPAY-2508: Move payment status to log; 1211f9c8
    YANDEXPAY-2495: Add standalone proxy for local-dev routing; a9e11dc8
    YANDEXPAY-2497: Fix preview on mobile; d39293d9
    YANDEXPAY-2497: Add playground to Docker-image; ec88626e
    YANDEXPAY-2497: Fix reset payment-button on settings change; 890a3bb2
[polrk]
    YANDEXPAY-2420: Add mobile styles; 1d7a7363
    YANDEXPAY-2420: Udpate tests; 3167d524
    YANDEXPAY-2420: Update components; 7f6522c0
    YANDEXPAY-2420: Remove code repeating; b0a6c789
    YANDEXPAY-2420: Add tests for playground; 111dc8c6
    YANDEXPAY-2489: Add LOG section; 1de7db4e
    YANDEXPAY-2482: Add shipping options; aec78180
    YANDEXPAY-2425: Add sidebar menu; 7029c572
    YANDEXPAY-2481: Add empty coupon validation; b0880a51
    YANDEXPAY-2477: Add timeout validation for coupon; 0324e978
    YANDEXPAY-2481: Промокод. Нет валидации на пустое поле (#406); 99fd3a54
## 0.26.0 (Tue Nov 02 2021 08:05:35 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2393: Add YaPay sdk exports; 53af1376
    YANDEXPAY-2393: Fix coupons usage on demo-page; 81cc64db
[ruslankunaev]
    YANDEXPAY-1812: Add user verification on checkout and FF enable for FF users; cb7bdf03
## 0.25.0 (Mon Nov 01 2021 12:54:17 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2421: Fix production build for playground service; b05398cf
    YANDEXPAY-2407: Define ym_uid cookie by sdk config; 11f0a2b6
    YANDEXPAY-2407: Add common id for Metrika logs; 9ea9e269
[polrk]
    YANDEXPAY-2393: Extract coupons getter; 047d7d24
    YANDEXPAY-2393: Code style; 31f4f94a
    YANDEXPAY-2393: Log error if is an unexpected; c7ce156a
    YANDEXPAY-2393: Check value before send; eb839cce
    YANDEXPAY-2393: Update communication logic; 4abb28a8
    YANDEXPAY-2393: Close coupon form; 4452861e
    YANDEXPAY-2393: Add coupon routes; b715584b
    YANDEXPAY-2393: Add coupon page; 60f634aa
    YANDEXPAY-2393: Add coupon form; bf9fbb94
    YANDEXPAY-2393: send coupon change to sdk; 34787239
    YANDEXPAY-2393: Add store for coupons; 1af5023a
    YANDEXPAY-2393: Add counters for coupon page; 248d0286
    YANDEXPAY-2393: Add coupon validation on client; e06d0b30
    YANDEXPAY-2393: Add merchant errors; b7b346a9
    YANDEXPAY-2393: Update button styles; 7f81f0b3
    YANDEXPAY-2393: Reject for specific error; aba1083e
    YANDEXPAY-2393: Update jsdoc; 3bd09476
    YANDEXPAY-2393: Send user coupon to the sdk; 888e8f1a
    YANDEXPAY-2393: Use strict mode; 508c0eee
    YANDEXPAY-2393: Send coupon to check out page; d9900868
    YANDEXPAY-2393: Add Coupon type; cc807bcb
    YANDEXPAY-2421: Update version range; 0fe27c5d
    YANDEXPAY-2421: Make react deps as peer deps; 78802bfa
    YANDEXPAY-2421: Add basic app layout; e5ca08bd
    YANDEXPAY-2421: Add favicons; dd15f8e8
    YANDEXPAY-2421: Remove console.log; da638d8f
    YANDEXPAY-2421: Add playground service; e2f9f9b6
    YANDEXPAY-2421: Simplify ts webpack loader; 40c20a05
    YANDEXPAY-2421: Remove hot update (call twice); e43ce7f6
    YANDEXPAY-2421: Add experimental scss loader; ee1491e3
    YANDEXPAY-2421: Update function name; 8c293668
    YANDEXPAY-2421: Update dependencies; 37b5f6d2
[ruslankunaev]
    YANDEXPAY-2440 Map refactor but with old architecture; 4237492c
    YANDEXPAY-2437 Add encoding to browser-info; c11656d6
    YANDEXPAY-2440 Map refactor; bd7c41d3
[sudilovskiy]
    YANDEXPAY-2411: Use exact version; 5c464258
    YANDEXPAY-2411: Fix missing tests dependencies; 5a679c2f
    YANDEXPAY-2411: Fix jest config path; 013173f0
    YANDEXPAY-2411: Fix transformer import; 44dbc7f7
    YANDEXPAY-2411: Fix node env detection; 1cfbcf24
    YANDEXPAY-2411: Return missing 'resolveConfig'; 2c51be70
    YANDEXPAY-2411: Replace '@pay-admin/config' package; b41d6632
    YANDEXPAY-2411: Add '@yandex-pay/testing-utils' package; 6418114a
    YANDEXPAY-2411: Ignore 'package-lock.json' in 'packages'; 6e1bc242
    YANDEXPAY-2411: Add jest config to 'checkout'; 2675e42b
    YANDEXPAY-2411: Add '@types/jest'; 75fb32b7
    YANDEXPAY-2411: Setup Jest tests run; 658f015f
    YANDEXPAY-2411: Add 'getShippingAddressMock'; 3a436bbe
    YANDEXPAY-2411: Add 'OpenerMock'; cbba2914
    YANDEXPAY-2411: Move 'getListener'; 2b1a10b1
    YANDEXPAY-2411: Add '@yandex-pay/testing-utils.mocks.mockWindow'; 7672d978
    YANDEXPAY-2411: Move '@yandex-pay/testing-utils' deps to 'peerDependencies'; ffae823c
    YANDEXPAY-2411: Add '@yandex-pay/testing-utils' index; d7b62036
    YANDEXPAY-2411: Add 'getPickupOptionsEventMock'; a1b8b92f
    YANDEXPAY-2411: Add 'getShippingOptionsEventMock'; e0bc8462
    YANDEXPAY-2411: Add 'getOrderEventMock'; cbb5bb15
    YANDEXPAY-2411: Add 'getEventMock'; fce5b4a0
    YANDEXPAY-2411: Add 'IConnectionMessage'; 2afa4fb0
    YANDEXPAY-2411: Add 'getPickupOptionMock'; 1eedd591
    YANDEXPAY-2411: Add 'getShippingOptionMock'; b3edad7b
    YANDEXPAY-2411: Add 'getOrderMock'; 214f7c7d
    YANDEXPAY-2411: Move 'getWindowMock' to package; d839673a
    YANDEXPAY-2411: Extract 'getWindowMock'; e15a9738
    YANDEXPAY-2411: Add '@yandex-pay/testing-utils' package; 95b34e79
## 0.24.0 (Fri Oct 22 2021 10:54:53 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2410: Fix cart items sort; c6a1bbcc
    YANDEXPAY-2408: Fix byttonType sdk-ready event; 7e82fd7c
    YANDEXPAY-2217: Hide preloader on error modal; 6f88f056
    YANDEXPAY-2346: Update quantity interface; 29d00b16
    YANDEXPAY-2400: Fix sending payment_start from pay-form; 954a7ec5
    YANDEXPAY-2400: Add delay to send process and checkout events; 8dc25865
    YANDEXPAY-2359: Add TVM for addrs.yandex.ru; 24f90fe3
[kir-9]
    YANDEXPAY-2217: Cheap test shipping error; 2a72b762
    YANDEXPAY-2217: Add error screens on rpc requests; cd772b35
    YANDEXPAY-2217: Fix long url refresh error; 72aebd63
    YANDEXPAY-2217: Add error screens on errors; 09c7b35f
    YANDEXPAY-2371: Sort order items; e33647cd
    YANDEXPAY-2371: Add discount order item type; 0b3f4f3c
    YANDEXPAY-2346: Add quantity to order item; 21c85e7c
    YANDEXPAY-2297: Add reset event on checkout form; aebe9017
[ruslankunaev]
    YANDEXPAY-2359: Add geocoder to server (addrs.yandex.ru); a74727a0
[sudilovskiy]
    YANDEXPAY-2349: Add npm script description; 67e6cfbf
    YANDEXPAY-2349: Add NPM cleanup script after install; 1d359cde
    YANDEXPAY-2349: Remove hot loader from production bundle; d33d0e1c
    YANDEXPAY-2349: Bump 'typescript' version; fcfca077
    YANDEXPAY-2349: Fix '@yandex-int/express-yandex-csp' compatibility; 28a5d48d
    YANDEXPAY-2349: Bump '@yandex-int/express-yandex-csp'; 39307c96
## 0.23.0 (Fri Oct 15 2021 07:34:43 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-2360: Add checkout button exp; 6772bc1d
    YANDEXPAY-2261: Fix imports; 6b339c2c
    YANDEXPAY-2261: Do not show checkout button in webview; 99dfd8c7
[stepler]
    YANDEXPAY-2343: Update README; d4f4f178
    YANDEXPAY-2343: Update local cert; 35dd1e00
## 0.22.0 (Mon Oct 11 2021 15:27:19 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2101: Update payment flow on demo-page; 59655105
    YANDEXPAY-2101: Ignore abort-event on close form from sdk; fc37ce63
[kir-9]
    YANDEXPAY-2281: Currency USD, EUR; 80bae819
## 0.21.0 (Mon Oct 11 2021 08:50:44 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-2283: Update checkout counters; 25f69d6a
    YANDEXPAY-2277: Correct address on change; 31ee5a8b
    YANDEXPAY-2228: Update address view; 3c02e4b7
    YANDEXPAY-2270: Save card in user_settings; 5ba875e9
## 0.20.0 (Thu Oct 07 2021 15:17:00 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2290: Fix uaas for sdk-init route; 6502a5f6
    YANDEXPAY-2289: Add debug logs; cc39a0c3
    YANDEXPAY-2101: Fix exp; 1f6bf022
## 0.19.0 (Tue Oct 05 2021 12:14:15 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2101: Update page focus warn message; 786136f1
    YANDEXPAY-2101: Fix ios/webview exp; a74ae2a8
[kir-9]
    YANDEXPAY-2258: Fix passport contact in list; 01ff33e3
## 0.18.0 (Tue Oct 05 2021 09:25:46 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2101: Fix ios/webview exp; 157bd0aa
[kir-9]
    YANDEXPAY-2260: Fix json.parse on delete request; 81b14e3a
[polrk]
    Update certs for local development; a9a1db4f
## 0.17.0 (Thu Sep 30 2021 08:25:37 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2241: Update contact duplicate logic; c5801e05
[polrk]
    YANDEXPAY-2094: Fix do not use pin; 52c36340
    YANDEXPAY-2094: Fix use ref target instead of ref; ce0fb268
    YANDEXPAY-2238: Fix infinite update; 14c933c2
## 0.16.0 (Wed Sep 29 2021 21:38:04 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2235: Remove api2; cb3a1c5c
    YANDEXPAY-2234: Fix map init race condition; fe0276ca
## 0.15.0 (Wed Sep 29 2021 18:08:54 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2233: Update main touch styles; a2730ca2
    YANDEXPAY-2224: Fix conditional hooks; 2ef85908
    YANDEXPAY-2225: Fix redirect; dbb012c6
    YANDEXPAY-2188: Update UI texts and messages; 7039d31a
    YANDEXPAY-2188: Add big-boss to FF; 2ef09bb1
    YANDEXPAY-2218: Select cheapest couries delivery; acf17998
    YANDEXPAY-2187: Update ob-flow on geo-address; 3774ee3c
[kir-9]
    YANDEXPAY-2224: Fix layout size; 3865464b
    YANDEXPAY-2227: Update onboarding; fb252ae2
    YANDEXPAY-2219: Select existing address on update; 8d95d768
    YANDEXPAY-2231: Fix reset cashback; ca04a535
    YANDEXPAY-2219: Select existing address on create; 930b1783
    YANDEXPAY-2216: Time log rpc requests; b3902f00
    YANDEXPAY-2214: Update change passport contact; 1f3a3ad3
    YANDEXPAY-2130: Update checkout pay button without avatar; 75a2230e
    YANDEXPAY-2213: Fix dublicate on save; 56efc9fb
## 0.14.0 (Wed Sep 29 2021 07:31:10 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2215: Update package-lock; 2ad11be5
    YANDEXPAY-2215: Remove checkout-mock service; 63f92724
    YANDEXPAY-2215: Remove unuser checkout code; 1e8b0b65
    YANDEXPAY-2212: Fix back url from onboarding contact page; 0ac48a75
    YANDEXPAY-2210: Fix selecting first address; 86510315
    YANDEXPAY-1850: Add required fields to meta info; 7df73151
    YANDEXPAY-2178: Add lastName and firstName to first contact form; 327b39f7
    YANDEXPAY-2159: Add Cash payment to demo payment-sheet; 17ee3ee6
    YANDEXPAY-2159: Show cash payment by payment-sheet; 8392a1ac
    YANDEXPAY-2159: Rename bay-button for cash payment; 856df533
    YANDEXPAY-2188: Fix deleting not-owned items; 7bf3d8e2
    YANDEXPAY-2188: Fix typo; 1bf99bef
    YANDEXPAY-2188: Fix editing not-owned items; 65a6b5e0
    YANDEXPAY-2188: Show onboarding address edit form if geo-address seletected; 43cf947b
    YANDEXPAY-2178: Add initial-fill for new contact form; 4cca314e
    YANDEXPAY-2203: Return payment data from checkout; 22763727
    YANDEXPAY-2203: Update sdk typings; 064d2ea5
    YANDEXPAY-2197: Get geo-api host from config; c1e33110
    YANDEXPAY-2139: Fix get-env function; 97e062bd
    YANDEXPAY-2139: Fix api2 prefix; ece75c63
    YANDEXPAY-2139: Add csrf for api2; 31b75a15
    YANDEXPAY-2139: Fix detect FF users; aae4f162
    YANDEXPAY-2140: Fix render for prod; baa178e4
    YANDEXPAY-2140: Remove scroll expanders; 825f8086
    YANDEXPAY-2140: Fix Map on touch; 1e92d0b9
    YANDEXPAY-2186: Fix typo in pay-form; 416c7500
    YANDEXPAY-2180: Fix checkout request on pay-form; 7020fccf
    YANDEXPAY-2160: Add reset user state btn; 8f994e5d
    YANDEXPAY-2160: Fix onboarding flow; cec7cbb9
    YANDEXPAY-2160: Add email and phone validation for contact form; 67d3144c
    YANDEXPAY-2160: Add transform parsers for api-data; d1848884
    YANDEXPAY-2102: Add lock-icont on desktop cart; d13bdf27
    YANDEXPAY-2140: Disable pay-button on missing payment data; 82a671a7
    YANDEXPAY-2102: Add select shipping preloader; f3dcb656
    YANDEXPAY-2147: Update onboarding flow; d6113d12
    YANDEXPAY-2140: Fix icons gradient; a7feb71c
    YANDEXPAY-2148: Fix SPA routes; 2efcb0a0
    YANDEXPAY-2102: Fix svg inline duplicates; d2a6e203
    YANDEXPAY-1852: Replace addresses for checkout-mock; 27dd9606
    YANDEXPAY-1851: Add shipping scenarios; 5a25f56b
    YANDEXPAY-1853: Restore error-icon; 960b6865
    YANDEXPAY-2139: Add route for checkout-mock; 85531752
    YANDEXPAY-2139: Add FF whitelist; 081ef0d6
    YANDEXPAY-2102: Raname paymentKey => paymentId; b556bfe6
    YANDEXPAY-1678: Add shipping requests; 3139bffc
    YANDEXPAY-2122: Remove initial mock; 6a287a1f
    YANDEXPAY-2122: Update forms; 871ec86c
    YANDEXPAY-2122: Add pay-api requests; 8a6684c4
    YANDEXPAY-2123: Add onboarding; 51109320
    YANDEXPAY-2102: Save query-params through routing; e1261afe
    YANDEXPAY-2102: Rewrite touch main page; 81c1a308
    YANDEXPAY-2102: Add scroll for drawer; 5d2c953d
    YANDEXPAY-2102: Add scroll and stycky footer; bd82c65c
    YANDEXPAY-2102: Fix panel layout; 92c8ab9b
    YANDEXPAY-2070: Remove old pages; 1bdc1b44
    YANDEXPAY-2070: Add pages with layout; f96f51a8
    YANDEXPAY-2070: Update std components; 50fb06fa
    YANDEXPAY-2070: Add panel and layout components; ac01a733
    YANDEXPAY-2013: Fix local proxy and redirect; b0f2b9f9
    YANDEXPAY-1852: Add auth redirect for checkout-mock; 70722d79
    YANDEXPAY-1852: Add checkout-mock routing to nginx config; 5b94378f
    YANDEXPAY-2096: Fix build mobile-api-assets; 6d94f5f6
    YANDEXPAY-2096: Add build script; 427f34f3
    YANDEXPAY-1852: Replace checkout url in dev-mode; ea6dbcb5
    YANDEXPAY-1852: Add checkout-mock form; cd98a32e
    YANDEXPAY-1852: Add checkout to sdk; d2487469
    YANDEXPAY-1852: Fix typings; d284d64c
    YANDEXPAY-1852: Add checkout typings; 22bac6be
    YANDEXPAY-2065: Add router; 18d37ac7
    YANDEXPAY-2011: Fix checkout; 6d4ba01f
    YANDEXPAY-2063: Apply linter rules; 5b2f6f9c
    YANDEXPAY-2011: Update README; 525520ab
    YANDEXPAY-2013: Remove old configs; c3872d2e
    YANDEXPAY-2063: Update linters; 8cbba456
    YANDEXPAY-2011: Update package-lock; 33b5dc34
    YANDEXPAY-2010: Add npm7 for server; 5861dc66
    YANDEXPAY-2012: Add HOT; 832a9a79
    YANDEXPAY-2013: Rewtire local services launch; 9996731f
    YANDEXPAY-2011: Fix building; 4bec2a92
    YANDEXPAY-2011: Migrate on npm7, webpack5 and babel; acf98f78
    YANDEXPAY-2010: Use npm7 and nginx-yasm image; 467f38ff
    YANDEXPAY-2010: Add NPM 7; 29be31a0
    YANDEXPAY-1724: Add yasm for proxy only; f21f386a
    YANDEXPAY-1724: Add signals with detailed request status; 2a76f7f6
    YANDEXPAY-1990: Add create address form; 1099933a
    YANDEXPAY-1843: Add address-list page; 2af50496
    YANDEXPAY-1843: Update base components; ee4842da
    YANDEXPAY-1843: Add addreses store; 8de551b1
    YANDEXPAY-1776: Add list-button component interface; 4a0be91b
    YANDEXPAY-1776: Fixes by review; 3fe71a82
    YANDEXPAY-1776: Update package-lock; 9c71e274
    YANDEXPAY-1776: Fix lint errors in checkout service; 5bff5b39
    YANDEXPAY-1878: Migrate api, libs, helpers and store from pay-form; dfc119b8
    YANDEXPAY-1849: Replace pay-form service by checkout; 1af2a47e
    YANDEXPAY-1879: Add react-services package; c6061aa7
    YANDEXPAY-1776: Fix lint errors in checkout service; 6457a48f
[kir-9]
    YANDEXPAY-2102: Add input mask; 5cf3e1e4
    YANDEXPAY-2140: Update checkout button; a35d9f5c
    YANDEXPAY-2210: Select first home address; 69f43389
    YANDEXPAY-2174: Fix autofill styles; af392fd7
    YANDEXPAY-2140: Update brandshop logo; 2a5148a0
    YANDEXPAY-2145: Add grouped addresses; dc4b1e19
    YANDEXPAY-2145: Sort addresses list; 11bdd850
    YANDEXPAY-2140: Fix fullscreen overflow; 993a1266
    YANDEXPAY-2130: Add checkout pay button; 1f431b7e
    YANDEXPAY-2185: Start checkout page with api; 8e64d962
    YANDEXPAY-2184: Start checkout step; 5990d55e
    YANDEXPAY-2140: Fix yapay badge; dbe35c96
    YANDEXPAY-2181: Fix load cashback; 3b1f1002
    YANDEXPAY-2193: Fix reset ob steps; 358e3728
    YANDEXPAY-2173: Fix card binding modal width; e9a6d766
    YANDEXPAY-2156: Disable drag for drawer; 0174009b
    YANDEXPAY-2140: Fix Panel Footer position; 774db077
    YANDEXPAY-2140: Fix amount with icon; 5683743c
    YANDEXPAY-2140: Add brandshop logo; 25c182b1
    YANDEXPAY-2175: Fix desktop block width; 3d7df3c0
    YANDEXPAY-2169: Fix nowrap in cart; c8fed62f
    YANDEXPAY-2157: Add width to main blocks; c48a1c3f
    YANDEXPAY-2102: Update checkout action; 9dbddbd0
    YANDEXPAY-2152: Add shipping select page; e10034a6
    YANDEXPAY-2151: Fix ob layout; 17ba3ccb
    YANDEXPAY-2140: Await save user state; 3aec5f0a
    YANDEXPAY-2140: Desktop blocks width; 75de5a00
    YANDEXPAY-2140: Save only on selected; 40562cda
    YANDEXPAY-2102: Add secure info blocks; 903f5d79
    YANDEXPAY-2102: Add user logo on ob header; d4d78b7f
    YANDEXPAY-1848: Update binding page; de8c4bdf
    YANDEXPAY-2098: Add remove modal to components; d9e3d54b
    YANDEXPAY-2098: Add remove modal; 4d7ec712
    YANDEXPAY-2102: Add bank icons; 841da838
    YANDEXPAY-1853: Add Loader; e25cd2e1
    YANDEXPAY-1853: Add ErrorScreen; 038b2da3
    YANDEXPAY-2102: Add disable prop to ListButtonRadio; d7b9c861
    YANDEXPAY-2102: Add icons; 4ccc6c81
    YANDEXPAY-2102: Update styles; dc0c2e2e
    YANDEXPAY-2102: Update main list-button; 875057de
    YANDEXPAY-2102: Update modal styles; d79ffada
    YANDEXPAY-2102: Add button variant primary; eebe69ab
    YANDEXPAY-1849: Main page; f431b951
    YANDEXPAY-1849: Add main page desktop; 1300de75
    YANDEXPAY-1849: Show plus cashback on main page; 84d848b2
    YANDEXPAY-1849: Add cart menu; 140e5bce
    YANDEXPAY-1849: Add main screen touch; 9198eda5
    YANDEXPAY-1847: Add new card payment; 0d473a37
    YANDEXPAY-1847: Add payment methods page; cd3d4aa2
    YANDEXPAY-1847: Update ListButton component; 7cc14e61
    YANDEXPAY-2072: Improve proxy; c91477c2
    YANDEXPAY-1844: Update contacts pages; 42370360
    YANDEXPAY-1844: Update addresses pages; 5226185a
    YANDEXPAY-1844: Add contacts store; 3959d269
    YANDEXPAY-1991: Update ListButton component; a76139d1
    YANDEXPAY-1776: Update ui components; 1108e130
    Add checkout service; d60aeec1
[polrk]
    YANDEXPAY-2196: Show placemark at selected address coords; d2f3e959
    YANDEXPAY-2196: Do not call set state if map is not mounted; afa73b54
    YANDEXPAY-2196: Refactor remove extra using map context; 16852187
    YANDEXPAY-2196: Refactor styles; fbe3c7ac
    YANDEXPAY-2196: Refactor duplicates; 05920185
    YANDEXPAY-2196: Add placemarks support; d2ad41d2
    YANDEXPAY-2196: Доработать показ карты на десктопе; 241e3440
    YANDEXPAY-2176: Show map on contacts pages; 54d33462
    YANDEXPAY-2176: Show map on contacts pages; 12640ce5
    YANDEXPAY-2153: Extract values into variables; 4832ed3e
    YANDEXPAY-2153: Update map behaviour; 9b77c08f
    YANDEXPAY-2095: Use exact version of module; b4911a3b
    YANDEXPAY-2095: Move map into features; 2372a375
    YANDEXPAY-2095: Move map context into features; 16c8c3e5
    YANDEXPAY-2095: rename variable; 80950cf1
    YANDEXPAY-2095: Extract pin icon; 7334d41b
    YANDEXPAY-2095: Fix use internal function for navigation; 701a4183
    YANDEXPAY-2095: Show pin while adding/editing; c8e51533
    YANDEXPAY-2095: Insert Map; c5c205fb
    YANDEXPAY-2095: Update addresses selectors; 0a83d093
    YANDEXPAY-2095: Update address type; add168a4
    YANDEXPAY-2095: Wrap app with map provider; 6d26d080
    YANDEXPAY-2095: Add MapContext; 4c01d66d
    YANDEXPAY-2117: rename files; f2168dd1
    YANDEXPAY-2117: Add class for address suggest item; 069e4cb9
    YANDEXPAY-2117: Remove unused styles; f1a16e6d
    YANDEXPAY-2117: Remove unused logic; d8517ea7
    YANDEXPAY-2117: Simplify menu select; 23434ef0
    YANDEXPAY-2117: Use new address selector; 83bcac52
    YANDEXPAY-2117: Add address selector; 71d8d9f0
    YANDEXPAY-2117: Delete old select search; 4d6cc70f
    YANDEXPAY-2117: Add debounce for input; f86f8530
    YANDEXPAY-2117: Update input with suggest; 80096332
    YANDEXPAY-2117: Update mock api; 761e8bad
    YANDEXPAY-2117: Add geocode API; 941aefe5
    YANDEXPAY-2117: Add input-with-suggest; 1d231ef0
    YANDEXPAY-2117: Add outside-click-wrapper; 4550e48a
    YANDEXPAY-2094: Update pickup page; 15af528f
    YANDEXPAY-2094: Fix eslint import order; 47f6ecfa
    YANDEXPAY-2094: Update yandex maps sdk imports; f2554549
    YANDEXPAY-2094: Handle errors in map component; 49ebc1c8
    YANDEXPAY-2094: Export map cn; 766c4c42
    YANDEXPAY-2094: Use exact package version; b734f953
    YANDEXPAY-2094: Fix pickup logic; ddd4752e
    YANDEXPAY-2094: Remove coordinates from mock data; 6e6cc137
    YANDEXPAY-2094: Update import names; a42af8be
    YANDEXPAY-2094: Add extra comments; 9a8222db
    YANDEXPAY-2094: Update pickup state; cfa5c675
    YANDEXPAY-2094: Add map component; c2d02cf4
    YANDEXPAY-2094: Update project linters; cd857260
    YANDEXPAY-2094: Fix remove only on ready instance; 5bd66894
    YANDEXPAY-2094: Add selecting functionality; 4cceadf4
    YANDEXPAY-2094: Remove double placemarks adding; 6dd4211f
    YANDEXPAY-2094: Add clusterization support; dcebb901
    YANDEXPAY-2094: Add mock datas; 823ae24c
    YANDEXPAY-2094: Fix typo; 892013a6
    YANDEXPAY-2094: Use existing object; a0e538ea
    YANDEXPAY-2094: Ignore ts error; 8443bcda
    YANDEXPAY-2094: Update blackbox host; 546bc61d
    YANDEXPAY-2094: Update lock file; c9eea150
    YANDEXPAY-2094: Update map creating; 3fd72668
    YANDEXPAY-2094: Add pickup store; f8390d15
    YANDEXPAY-2094: Add mock api for pickup options; a5b7de6c
    YANDEXPAY-2094: Export async data status; 6b56a068
    YANDEXPAY-2094: Remove debug mode on testing; bb7d1688
    YANDEXPAY-2094: Extract api key from string; e88318e1
    YANDEXPAY-2094: Fix cleanup; 68e9fc39
    YANDEXPAY-2094: Update map styles; e7094ce0
    YANDEXPAY-2094: Update typings; 660138df
    YANDEXPAY-2094: Add routes for pickup page; 669f7783
    YANDEXPAY-2094: Add pickup page; e32ceca0
    YANDEXPAY-2094: Update webpack config; 85ac2d61
    YANDEXPAY-2094: Add ymaps js sdk; 700a0fd5
    Update redirect; 44d0982a
    Fix typo; 79ee180c
    Update scripts start with npm7; 6714432d
    Add support on before middleware; 2de4d19a
    Add one click IDE startup scripts; e7903285
    Update procfile for npm 7; 7e3362a3
    Update lock file; 726309eb
## 0.13.0 (Mon Sep 27 2021 12:23:18 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2199: Update robokassa icon; a16145a
    YANDEXPAY-2101: Add sync exps; 1a5628d
    YANDEXPAY-2101: Increase timeout to process; d2369c1
[kir-9]
    YANDEXPAY-2101: Add experiment immediate-close-form; 13a0e52
    YANDEXPAY-2101: Close form after payment process; 5abeccb
## 0.12.0 (Thu Sep 16 2021 07:51:22 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2082: Disable channels in utils/connection; b77a13d
## 0.11.0 (Mon Sep 13 2021 12:53:29 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-2045: Fix pay via redirects on sandbox; 5379741
    YANDEXPAY-2023: Add custom settings on demo via query params; 83ed9c1
[nyanbear]
    Fix AT case 76 - add waiting for item loads; a228a93
    Update screenshots; e97fdbd
    Waiting for items to load; 9250e25
    Delete const user; ead283e
    Rename test-data; 0686b5a
    Fix AT case 76; bac0c61
    Fix AT case 72; 6c42f6c
    Fix AT case 48; 437e988
    Fix AT case 122; 6ee9f5d
    Fix AT case 52; 031500c
    Fix AT case 73; 8a7317b
    Fix AT case 47-49; 455a5c2
    Fix AT case 130; 45c3d21
    Fix AT case 176; 513ea2f
    Fix AT case 118; ea78a46
    Fix AT case 47; 999a78d
    Fix AT case 119; ce57adb
    Fix AT case 113; 36246f4
    Fix AT case 48; 43ed408
    Fix AT case 63; eede6f4
    Config and test-data change; e691dbe
    Fix AutoTests; e26286c
[kir-9]
    YANDEXPAY-1604: Fix iOS button not clicked; 6feab85
[Suschev.Artem]
    YANDEXPAY-1724 decoupled web-service and nginx unistat configs; 79bde30
    YANDEXPAY-1724 nginx unistat; 4f17d64
## 0.10.0 (Thu Sep 02 2021 15:00:08 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-1999: Replace Robokassa icon; 5cc5d9d
    YANDEXPAY-1943: Start tvmtool separately; d998ca8
    YANDEXPAY-1943: Add start script to package.json; 770e9d0
## 0.9.0 (Fri Aug 27 2021 09:20:10 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-1805: Add amount update on demo-page; c298c45
    YANDEXPAY-1805: Rerender button on payment update; 0f23e31
    YANDEXPAY-1805: Use paymentSheet instead paymetData; 6aba7fb
    YANDEXPAY-1805: Emit payment-method update on update payment; 471c572
    YANDEXPAY-1931: Update README; 4a96350
    YANDEXPAY-1931: Add copy-cert script; d5b0689
[vladislavteli]
    YANDEXPAY-1805: После payment.update не обновляется количество кэшбэка; 91564f0
## 0.8.0 (Wed Aug 25 2021 17:36:27 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-1913: Fix tele2 badge size; ee4c2ae
    YANDEXPAY-1913: Add gift-badge on demo page; 5ed0471
    YANDEXPAY-1913: Add Tele2 badge; 97c0ecc
    YANDEXPAY-1913: Replace icons by common component; bf28f7d
    YANDEXPAY-1913: Disable RUM logs for development mode; 16796d9
    YANDEXPAY-1836: Fixes by review; a58e667
    YANDEXPAY-1807: Refactor tracking for binding; 1ffac90
[vladislavteli]
    YANDEXPAY-1836: [front] Доработать ручку isReadyToPay; 5b89612
[kir-9]
    YANDEXPAY-1807: Update binding counters; c165627
    YANDEXPAY-1783: Fix unavailable localStorage error; 6f507a9
## 0.7.0 (Mon Aug 16 2021 09:16:08 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-1799: Поддержка белорусского рубля; c0c2e8f
    YANDEXPAY-1704: Hide track user route; 701039f
## 0.6.0 (Fri Aug 06 2021 14:40:34 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-1665: Fix robokassa logo; a294862
    YANDEXPAY-1665: Change robokassa tab icon; bbbb83e
[temasus]
    Add alerting to docs; e6e29c3
## 0.5.0 (Fri Jul 30 2021 11:50:53 GMT+0000 (Coordinated Universal Time))

[kir-9]
    YANDEXPAY-1753: Fix legal link view; 576d1a7
    YANDEXPAY-1735: Fix touch scroll to email; 1682f00
    YANDEXPAY-1754: Fix text in button in touch; dc1b395
    YANDEXPAY-1738: Fix plus crossbrowser view; b62f9bb
    YANDEXPAY-1729: Remove replace param from openWindow; 64eca47
    YANDEXPAY-1613: Add cardId param to cashback request; d5b1721
    YANDEXPAY-1664: Add plus agreement link; 4a4b472
    YANDEXPAY-1613: Add updating payment method with styles to demo; bc468a7
    YANDEXPAY-1615: Add button styles to payment method; 7883e35
    YANDEXPAY-1617: Add plus cashback to pay form; 70ccc1d
    YANDEXPAY-1619: Show simple button in frame; edeed32
    YANDEXPAY-1615: Add plus cashback to button; 4e7453f
    YANDEXPAY-1613: Add cashback route mock; 19ddd45
    YANDEXPAY-1613: Add cashback route; 4771d59
    YANDEXPAY-1735: Add scroll to email input on focus; ebb2543
    YANDEXPAY-1668: Update demo-page; d0a8cf9
    YANDEXPAY-1668: Update docs; 3d285c4
    YANDEXPAY-1668: Update lego-components; bbcd476
    YANDEXPAY-1668: Add email to pay form; 1333dab
    YANDEXPAY-1668: Get email from blackbox; 53332b0
    YANDEXPAY-1668: Add BigInput component; b8a4025
    YANDEXPAY-1726: Add dom forEach; 21f6c1b
    YANDEXPAY-1726: Fix csp; f9f1a3f
    YANDEXPAY-1719: Set local vars with logic to function; 319b823
## 0.4.0 (Wed Jul 21 2021 11:56:01 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-1106: Add env and req_id params to CSP reports; 6c24035
    YANDEXPAY-1611: Apply exp local-save-card; 9d00e52
    YANDEXPAY-1656: Add web-api docs; d7bfef5
    YANDEXPAY-1656: Remove empty avatar from /web-api/mobile/v1/user_info; 43df7fc
[kir-9]
    YANDEXPAY-1106: Add tests; b555b83
    YANDEXPAY-1106: Move CSP config to configs; 3f252de
    YANDEXPAY-1106: Add CSP for testing; 6c63bf9
    YANDEXPAY-1106: Add dom observable; 2fdfc4a
## 0.3.0 (Tue Jul 13 2021 15:42:38 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-1109: Fix recreate button on same session; bab4a0d
    YANDEXPAY-1537: Add nginx configs; 88556da
    YANDEXPAY-1537: Move uatraits-data to base image; 81f97d5
    YANDEXPAY-1537: Reduce image size; cdf49a4
    YANDEXPAY-1537: Fix Docker base image name; e5b73a1
    YANDEXPAY-1488: Update fix for Android webview; ff49986
    YANDEXPAY-1109: Send sdk error logs via proxy; c2068b0
    YANDEXPAY-1109: Add error-log to sdk-init method; 52cc6b5
    YANDEXPAY-1620: Fix button render on undefined paymentSheet.order; cc49835
[kir-9]
    YANDEXPAY-1537: Add base docker from trust; e29485a
    YANDEXPAY-1637: Add delta-logger to sdk; 8166cfb
    YANDEXPAY-1637: Add delta-logger; 2cc7ac4
    YANDEXPAY-1109: Change log error from metrika to error-logger; 9e2bf54
    YANDEXPAY-1109: Add error-logger; 85bc48a
    YANDEXPAY-1109: Add sdk log; 60d2bbd
## 0.2.0 (Thu Jul 08 2021 21:21:31 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-1195: Use YandexPay service-token for binding; 28d371f
[kir-9]
    YANDEXPAY-1599: Fix frame 3ds size; b81a5a4
    YANDEXPAY-1584: Add render data logger; 33a5281
## 0.1.0 (Wed Jul 07 2021 15:58:15 GMT+0000 (Coordinated Universal Time))

[stepler]
    YANDEXPAY-1600: Add changelog; 1d44f63
[kir-9]
    YANDEXPAY-1458: Send merchant url and name to metrika; fb05854
    YANDEXPAY-1458: Add merchant.url; c489766
