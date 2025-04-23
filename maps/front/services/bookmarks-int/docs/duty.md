## Juggler alerts

### ban-violators

[Monitoring link](TODO)

This alert triggers every time when the service detects the violator
(the user who saved a big amount of the shared lists) and tries to ban him.
Once the alert notification was raised the duty engineer must do as follows:

1. Connect to the database cluster in the appropriate environment:
  - [Testing](https://yc.yandex-team.ru/folders/foonquium8istgt59qca/managed-postgresql/cluster/mdb2uc1v4p03679qq9f9)
  - [Production](https://yc.yandex-team.ru/folders/foonquium8istgt59qca/managed-postgresql/cluster/mdbvj64kc1kqctu95ud9)
2. Select all the new ban records:
  ```sql
  SELECT * FROM banned_violators WHERE reviewed = false
  ```
3. Manually review each of them, make a decision regarding the user's ban status (ban, unban, whitelist),
   and make appropriate changes in DB (using the `UPDATE` SQL command).
   **Important:** The `reviewed` flag must be set to `true` during this update:
    ```sql
    -- Keep user banned
    UPDATE banned_violators SET
      reviewed = true
    WHERE uid = <uid from banned_violators>

    -- OR add the user to the whitelist
    UPDATE banned_violators SET
      status = 'whitelisted',
      previous_status = <previous status of record>,
      exclusive_limit = <new exclusive limit>,
      reviewed = true
    WHERE uid = <uid from banned_violators>

    -- OR Unban user
    DELETE FROM banned_violators WHERE uid = <uid from banned_violators>
    ```
   The following steps might help you make a decision:
  - Select all the lists of the user, review them manually and
    try to predict if the user is a violator or he's just like to use our service:
    ```sql
    SELECT * FROM lists where uid = <uid from banned_violators>
    ```
4. That's it! The updates you made in DB will be delivered to the service instances in a few minutes,
   manual redeploy isn't required.
   The banned user won't update his shared lists anymore (create/delete/close), the rest functionality keeps as is.

### FAQ:

- Q: **I've got a lot of such alerts in a short time (or on the weekend / middle of the night).**
  **Should I drop all my current doings and start resolving this alert?**

  A: Usually - no. Keep your eye on the attendant alerts: If you'll see the service degradation
  started at the same time you got a `ban-violators` alert - it's worth to spend your time on this one first
  and ban all the violators. Probably the degradation will be stopped once the DB updates
  will be delivered to the service instances. If there is no degradation - it's OK to postpone
  resolving this alert to a few hours / morning / Monday.
- Q: **How long the DB updates will be delivered to the service instances?**

  A: We can determine the upper border of this time in milliseconds:
  `(Count of instances in the environment) * (Value of the 'app.banCacheRenewTimeoutMs' config property)`
- Q: **The user we've banned reached me / my manager / support folks and asking:**
  **"Why I can't update my shared lists? I always gaining the error!". What should I do?**

  A: Such kind of communication must be performed through the first-line support service.
  First of all, we have to explain to the user that we've banned him and why we had to do this.
  Then we might suggest him to delete all the junk he saved in our service and/or set the exclusive limit for him
  (we can do it manually as described above) and ask him to not exceed it anymore.
  If he will exceed this limit again - it's worth keeping him in the banned state forever
  (he'll still be able to subscribe on the lists and get its updates).
  This is the exclusive measure, it's worth discussing it with the service
  [manager / development team](https://abc.yandex-team.ru/services/maps-front-bookmarks-int/)
