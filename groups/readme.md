# Repository group
Repository group is a group of certain people for any project or subject of source code development in Arcadia.

### How to add group for my team
To change certain group commit to the appropriate `ya.make` file. 
Example: 
arcadia/devtools/sample_project/__ya.make__

```
...
OWNER(
    g:yatool
    rudskoy
    rnefyodov
    nalpp
    workfork
)
...
```



### How to validate ya.make group from console
* Use `ya make -t groups` (run this from Arcadia root) to check if your change is valid.

### Declaration ya.make file
* One file for one group
* File name should not contain dots

### Declaration group content (sample)
```
members = [
  "number_one",
  "number_two"
]

display_name = "Fancy name for your group"

mail = "<something>@yandex-team.ru"

```
Files are in `toml` format with the following keys:
* __members__: list of users. Each login should not contain `@` or `yandex-team.ru` at the end, and should be known to _Staff_. All the users should not be dismissed.
* __mail__: single email used by Arcanum and Review Board to notify the group. Only emails at `yandex-team.ru` are allowed.
* __display_name__: display name for the group, non-ascii symbols are not supported.

#### 'members = []' are
People are attended the repository project or subject field of work in company.
For example: 
* g:yt – group of YT developers
* g:yt-wrapper – group of YT developers responsible for YT-wrapper
* g:contrib – group of users that helps users to add and update arcadia/contrib

#### 'mail =' is
People are attended in review request have got all the notifications their emails.
All the notifications for people are duplicated on mail = "<something>@yandex-team.ru"


