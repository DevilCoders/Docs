# API саппорта почты

## Авторизация

Авторизация происходит с помощью TVM. Тикет передается HTTP заголовке запроса: `Ticket`.

Пример запроса: 

    POST /api/external/userinfo HTTP/1.1
    Host: magic.yandex-team.ru
    Ticket: <tvm_ticket>
    
    ...
    
#### Как получить доступ:

* Создать приложение в [TVM](https://tvm.yandex-team.ru)
* Получить client_id и public_key 
* Создать задачу для их добавления в очереди [MAGIC](https://st.yandex-team.ru/MAGIC)


## Информация о пользователе и blackbox

    POST /api/external/userinfo
    
 Параметры:
 
 * login - логин пользователя на Яндексе
 
 Пример ответа:
 
    {
      "status": "ok",
      "result": {
        "email": "test2017@yandex.ru",
        "login": "test2017",
        "uid": "4002173589",
        "karma": 0,
        "is_app_password_enabled": true,
        "is_2fa_on": false
      }
    }
    
    
## Настройки и параметры пользователя
    
    POST /api/external/settings

   Параметры:
 
 * login - логин пользователя на Яндексе
 
 Пример ответа:
 
    {
      "status": "ok",
      "result": {
           "settings" : {
              "parameters" : {
                 "single_settings" : {
                    "kcuf_comp" : "1403858956,185.6.245.156",
                    "qu_promo_app_p_a" : "%7B%22ws_show-count-all%22%3A1%2C%22ws_show-count%22%3A1%2C%22ws_close-count%22%3A0%2C%22ws_stage%22%3A%22show%22%2C%22ws_first-show%22%3A1471509517535%2C%22ws_last-show%22%3A1471509517535%7D",
                    "mail-in-browser" : "%7B%22firstStart%22%3A0%7D",
                    "quinn_visited" : "on",
                    "promo-manager" : "%7B%22last-time-show-promo%22%3A1492419104152%2C%22last-promo-was-name%22%3A%22yabrowser-promoline%22%7D",
                    "m_head_folded_sender" : "on",
                    "exp-32005" : "on",
                    "yabrowser_promo_date" : "1401545500153",
                    "u2709" : "on",
                    "exp-32359" : "on",
                    "last-login-ts" : "1472052843084",
                    "hide_daria_left" : "",
                    "boxBirthdayTimestamp" : "",
                    "no_collectors_bubble" : "on",
                    "no_reply_notify" : "",
                    "exp-34680" : "on",
                    "exp-32840" : "on",
                    "hk_promo_bubble" : "count=2&lastTS=1392551357155&codes=fe",
                    "mail_inbrowser_close" : "1405971055673",
                    "collect_not_24" : "1470912371153",
                    "liza_opened" : "on",
                    "has_inbox_message" : "on",
                    "wizard-mobile-done" : "2016-01-28T17:10:41/0",
                    "done_shown_counter" : "2",
                    "first-login-date" : "1391022899805",
                    "size-view-app2" : "0",
                    "flight_notify" : "true",
                    "alias-promo" : "%7B%22shown-on-done%22%3Atrue%7D",
                    "no_collect_bubbl_all" : "on",
                    "user_dropdown_promo" : "on",
                    "m_head_full_edition" : "on",
                    "tb_mail_mailbox_act" : "on",
                    "qu_last-time-promo" : "1471509517535",
                    "last_news" : "23",
                    "wizard-u2709" : "1453888069266",
                    "sound_message" : "on",
                    "exp-32556" : "on",
                    "hide_empty_folders" : "",
                    "messages_avatars" : "on",
                    "rph" : "mozilla=0&opera=0&webkit=1",
                    "show_checkbox_inside_userpic" : "on",
                    "rpop_backend" : "pq",
                    "noreply_popup_shown" : "on",
                    "localize_imap" : "on",
                    "quinn-push-promo" : "%7B%22success%22%3Afalse%2C%22twoweeks%22%3Afalse%2C%22threedays%22%3Atrue%2C%22timestamp%22%3A1471509525299%7D",
                    "open-message-list" : "",
                    "show_checkbox_inside-applied" : "on",
                    "liza_minified_header" : "",
                    "right_column_expanded" : ""
                 }
              },
              "profile" : {
                 "emails" : [
                    {
                       "date" : "2014-01-29 23:14:34",
                       "def" : false,
                       "rpop" : false,
                       "address" : "rubtsov.dmv@ya.ru",
                       "validated" : true,
                       "native" : true
                    },
                    {
                       "date" : "2014-01-29 23:14:34",
                       "def" : false,
                       "rpop" : false,
                       "address" : "rubtsov.dmv@yandex.by",
                       "validated" : true,
                       "native" : true
                    },
                    {
                       "date" : "2014-01-29 23:14:34",
                       "def" : false,
                       "rpop" : false,
                       "address" : "rubtsov.dmv@yandex.com",
                       "validated" : true,
                       "native" : true
                    },
                    {
                       "date" : "2014-01-29 23:14:34",
                       "def" : false,
                       "rpop" : false,
                       "address" : "rubtsov.dmv@yandex.kz",
                       "validated" : true,
                       "native" : true
                    },
                    {
                       "date" : "2014-01-29 23:14:34",
                       "def" : true,
                       "rpop" : false,
                       "address" : "rubtsov.dmv@yandex.ru",
                       "validated" : true,
                       "native" : true
                    },
                    {
                       "date" : "2014-01-29 23:14:34",
                       "def" : false,
                       "rpop" : false,
                       "address" : "rubtsov.dmv@yandex.ua",
                       "validated" : true,
                       "native" : true
                    }
                 ],
                 "single_settings" : {
                    "yandex_sign_enable" : "",
                    "subs_show_item" : "on",
                    "enable_pop" : "",
                    "imap_rename_enabled" : "",
                    "collect_addresses" : "on",
                    "no_firstline" : "",
                    "subs_show_unread" : "",
                    "no_advertisement" : "",
                    "disable_social_notification" : "",
                    "abook_page_size" : "50",
                    "enable_welcome_page" : "on",
                    "color_scheme" : "",
                    "have_seen_stamp" : "",
                    "enable_autosave" : "on",
                    "show_news" : "on",
                    "pop_spam_enable" : "on",
                    "translate" : "on",
                    "first_login" : "",
                    "signature_eng" : "",
                    "enable_images_in_spam" : "",
                    "new_interface_by_default" : "",
                    "messages_per_page" : "30",
                    "pop_spam_subject_mark_enable" : "on",
                    "https_enabled" : "on",
                    "hide_daria_header" : "",
                    "enable_social_notification" : "on",
                    "have_seen_daria" : "",
                    "show_stocks" : "",
                    "dont_delete_msg_from_imap" : "",
                    "label_sort" : "by_count",
                    "save_sent" : "on",
                    "use_small_fonts" : "",
                    "enable_firstline" : "on",
                    "pop3_max_download" : "50",
                    "broad_view" : "",
                    "jump_to_next_message" : "",
                    "duplicate_menu" : "",
                    "page_after_move" : "current_list",
                    "show_chat" : "",
                    "use_monospace_in_text" : "",
                    "show_unread" : "",
                    "enable_imap" : "on",
                    "suggest_addr_maxnum" : "500",
                    "subs_messages_per_page" : "20",
                    "show_weather" : "",
                    "page_after_send" : "done",
                    "pop3_archivate" : "on",
                    "from_name_eng" : "",
                    "show_advertisement" : "on",
                    "dnd_enabled" : "on",
                    "subs_show_line" : "on",
                    "pop3_makes_read" : "",
                    "no_mailbox_selection" : "",
                    "enable_mailbox_selection" : "on",
                    "mobile_messages_per_page" : "15",
                    "no_news" : "",
                    "mobile_sign" : "Отправлено из мобильной Яндекс.Почты: http://m.ya.ru/ymail",
                    "page_after_delete" : "current_list",
                    "folder_thread_view" : "on",
                    "hide_tip_for_video_letter" : "",
                    "signature" : "",
                    "ml_to_inbox" : "on",
                    "show_avatars" : "on",
                    "default_email" : "rubtsov.dmv@yandex.ru",
                    "daria_welcome_page" : "",
                    "show_todo" : "",
                    "from_name" : "Dmitry Rubtsov",
                    "copy_smtp_messages_to_sent" : "",
                    "enable_hotkeys" : "on",
                    "signature_top" : "",
                    "close_quoting" : "",
                    "skin_name" : "neo2",
                    "suggest_addresses" : "on",
                    "enable_quoting" : "on",
                    "enable_pop3_max_download" : "",
                    "default_mailbox" : "yandex.ru",
                    "enable_richedit" : "",
                    "subs_show_informer" : "on",
                    "interface_settings" : "",
                    "webchat_turned_off" : "",
                    "show_socnet_avatars" : "",
                    "quotation_char" : ">",
                    "enable_images" : "on",
                    "alert_on_empty_subject" : "on"
                 }
              }
           }
        }
    }

## Фильтры и форварды пользователя

    POST /api/external/filters
    
 Параметры:
 
 * login - логин пользователя на Яндексе
 
Пример ответа:

    {
      "status": "ok",
      "result": [
           {
             "priority" : 29,
             "actions" : [
                {
                   "parameter" : "pupkin@yandex-team.ru",
                   "verified" : true,
                   "type" : "notify"
                }
             ],
             "stop" : false,
             "name" : "Моё правило",
             "created" : 1443460534,
             "id" : "83251",
             "conditions" : [
                {
                   "link" : "1",
                   "div" : "nospam",
                   "oper" : 1
                },
                {
                   "link" : "0",
                   "pattern" : "pupkin@gmail.com",
                   "div" : "from",
                   "oper" : 1
                }
             ],
             "enabled" : true
          }
      ]
    }
     

В `result` передается спсисок всех фильтров.

Параметры фильтра:

* id - идентификатор фильра
* stop -  0 - применять последующие правила, 1 - не применять
* name - имя фильтра
* created - unixtime создания
* enabled - фильтр акитвен
* priority - приоритет применения правила
* conditions - список условий применения фильтра (см. [ниже](#Условия))
* actions - действия, которые применять к письмам (см. [ниже](#Действия))

Подробнее про фильтры можно прочитать [тут](https://wiki.yandex-team.ru/users/mio369/furita/).    

#### Условия 

Параметры условия:

* link - знак после условия 0 - объединение условий по ИЛИ, 1 - по И
* div - параметр письма, может принимать значения:
    * `nospam` - не спам `all` - спам и не спам `clearspam` - только спам
    * from/to/cc/subject/body/filename
    * имя заголовка письма
* oper - 1 - совпадает, 2 - не совпадает, 3 - содержит, 4 - не содержит
* pattern – строка к которое матчится поле

Первым условием, как правило (его может и не быть), идет условие, определяющее применять ли это письмо к спаму или нет.

**Ко всем письмам, кроме спама**

    {
       "link" : "1",
       "div" : "nospam",
       "oper" : 1
    }

**Ко всем письмам, включая спам**

    {
       "link" : "1",
       "div" : "all",
       "oper" : 1
    }


**Только к спаму**

    {
       "link" : "1",
       "div" : "clearspam",
       "oper" : 1
    }


#### Действия

Параметры действия:

* type - тип действия:
    * move - перемещение в папку (параметр: ID папки)
    * movel - пометка меткой (параметр: ID метки)
    * forward - пересылка на адрес (параметр: email пересылки)
    * forwardwithstore - пересылка на адрес с сохранением письма (параметр: email пересылки)
    * reply - автоответ (параметр: текст автоответа)
    * notify - уведомление по адресу notify_address (параметр: email уведомления)
    * status - пометить письмо (параметр: `ro` - прочитанным)
    * delete - удалить письмл
* parameter - паметр для действия (email, ID папки, текст автоответа)
* verified - действие подтверждено и активно


#### Примеры действий

**Форвард**

    {
       "parameter" : "pupkin@yandex-team.com",
       "verified" : true,
       "type" : "forward"
    }


**Форвард с сохранением**

    {
       "parameter" : "pupkin@yandex-team.com",
       "verified" : true,
       "type" : "forwardwithstore"
    }


**Пометить прочитанным**

    {
       "parameter" : "ro",
       "verified" : true,
       "type" : "status"
    }


**Удалить**

    {
       "verified" : true,
       "type" : "delete"
    }


**Переместить в папку**

    {
       "parameter" : "1",
       "verified" : true,
       "type" : "move"
    }


**Поставить метку**

    {
       "parameter" : "1",
       "verified" : true,
       "type" : "movel"
    }


**Уведомление**

    {
       "parameter" : "pupkin@yandex-team.ru",
       "verified" : true,
       "type" : "notify"
    }


**Автоответ**

    {
       "parameter" : "Меня нет дома",
       "verified" : true,
       "type" : "reply"
    }


 
## Блеклист пользователя

    POST /api/external/blacklist

 Параметры:
 
 * login - логин пользователя на Яндексе
 
Пример ответа:

    {
      "status": "ok",
      "result": ["no-reply@example.com"]
    }
     

## Логи почты (userjournal)

    POST /api/external/userjournal
    
Параметры:

* login - логин пользователя на Яндексе
* from_ts, to_ts - unixtime границы поиска логов
* limit - количесвто записей лога
* modules - список компонентов

Пример ответа:

    {
      "status": "ok",
      "result": [
            {
             "affected" : "1",
             "ip" : "188.166.95.178",
             "filterIds" : "384185",
             "date" : 1487100749990,
             "tid" : "161285161655390179",
             "state" : "List-Id=\"Python core developers <python-dev.python.org>\"",
             "mid" : "161285161655390185",
             "target" : "message",
             "fid" : "7",
             "operation" : "receive",
             "ftype" : "0",
             "emailFrom" : "brett@python.org",
             "module" : "fastsrv",
             "connectionId" : "FTvFjS4uT9-WGWGv3CT",
             "subject" : "Re: [Python-Dev] Update on labels to be used on GitHub",
             "msgId" : "<CAP1=2W5McdmENKjJGPo+DtoK06Ub8UYzE6_Hr0ZRjZGw3E-A5Q@mail.gmail.com>",
             "unixtime" : "1487100749",
             "suid" : "761498862",
             "labelSymbols" : ",recent_label,seen_label",
             "hidden" : "0",
             "stid" : "105398.761498862.284723375230952585955766357779",
             "mdb" : "pg"
        }
      ]
    }

Подробнее описано [тут](https://github.yandex-team.ru/mail-support/yandex-winx/blob/master/docs/userjournal.md).

## Сборщики 

    POST /api/external/collectors
    
Параметры:

* login - логин пользователя на Яндексе


Пример ответа:

    {
      "status": "ok",
      "result": [
          {
             "actions" : [
                "0"
             ],
             "popid" : "498465",
             "imap" : false,
             "abook_sync_state" : "0",
             "last_connect" : "1487514395",
             "email" : "example@yandex.ru",
             "last_msg_count" : 0,
             "server" : "pop.gmail.com",
             "is_ng" : "0",
             "leave_msgs" : true,
             "is_on" : "3",
             "session_duration" : "2",
             "port" : "995",
             "imap_root_folder" : "",
             "login" : "example@yandex.ru",
             "use_ssl" : true,
             "error_status" : "login error",
             "bad_retries" : 394
          }
      ]
    }

Описание параметров [API сборщиков](https://wiki.yandex-team.ru/Pochta/mx/yarm/#opisanieparametrov).


## Папки пользователя

    POST /api/external/folders
   
Параметры:

* login - логин пользователя на Яндексе

 
Пример ответа:

    {
      "status": "ok",
      "result": [
          {
             "name" : "Входящие",
             "fid" : 1,
             "messages" : 10,
             "messages_new" : 3,
             "messages_unread" : 3,
             "size" : 10,
             "pop3" : "on"
          }
      ]
    }
    
## Эксперименты пользователя

    POST /api/external/experiments
    
Параметры:

* login - логин пользователя на Яндексе

Пример ответа:

    {
      "status": "ok",
      "result": {"experiments": "53505,0,9;60671,0,54;55592,0,65"}
    }
