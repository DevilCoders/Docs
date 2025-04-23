Contains sample responses from server

Sample response

# Messages

    curl -v --header "Authorization: OAuth 8f28a27cc8de4963aef346dacd38b532" http://mail.yandex.ru/api/mobile/v1/messages -X POST -d '{"requests":[{"fid":"1","threaded":"false","first":"0","last":"100","md5":"as","returnIfModified":"true"}]}'

# Xlist

    curl -v --header "Authorization: OAuth c0ed10579479483893e5624db856f43b" http://mail.yandex.ru/api/mobile/v1/xlist