# robots-vertis-jawa
https://staff.yandex-team.ru/robot-vertis-jawa

## API

### Table of contents
* [Add Startrek issue to planning poker](#add-startrek-issue-to-planning-poker)
* [Process on-duty event on Startrek issue](#process-on-duty-event-on-startrek-issue)

### Add Startrek issue to planning poker
```
POST /triggers/issue/{ISSUE-KEY}/poker/{AGILE-BOARD-ID}
```

### Process on-duty event on Startrek issue
```
POST /triggers/issue/{ISSUE-KEY}/duty/{ABC-SCHEDULE-ID}
```

Settings in query (search) params:

* `summon: true/false` — should write an issue comment and summon on-duty user there
* `assign: true/false` — should assign on-duty user to issue 
