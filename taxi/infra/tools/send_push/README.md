Scripts for massive sending info pushes
============

If you want to send some info to Taxi Users using push notifications, you should make next steps:

  * Download user data. It should be given in Startrek ticket as a file with user ids.
  * Send pushes from a production server with script 
  `tools/send_push/send_by_uuids.sh user_ids.csv user "Текст пуша" ["<deeplink>'"] ["<promocodes_filename_>'"]`
  or
  `tools/send_push/send_by_uuids.sh phone_ids.csv phone "Текст пуша" ["<deeplink>'"] ["<promocodes_filename_>'"]`
  ,
  where `deeplink` is string like 'yandextaxi://addcreditcard' or 'yandextaxi://addpromocode?code=SOMECODE'
  and `promocodes_filename` is name of file with unique promocodes (each on separate line).
  If promocodes are given then deeplink is ignored (use `""` in this case).
  It prints stats about sending process on the screen and uses `pushkin.py` as library.
  * If there were errors they are stored in *.errors files. You can resend them.
  * Get *.delivered and *.undelivered files from production server and attach them to Startrek ticket.

For more information look file's docstrings  in current directory and read the code.
Ask some questions khlyzov@.

**NOTE:** You should understand that sending many thousands of pushes can increase load to servers from users that open their apps.
So maybe we should distribute pushes in quite longer time. Yet, that is for managers to decide.
