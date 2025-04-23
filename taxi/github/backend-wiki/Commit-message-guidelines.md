### Example (single commit message)

```
bug admin: remove 'protocol' from logs

Meta-parameter 'protocol' is no longer saved in log documents. Admin site should rely on other indicators to properly format request/response bodies.

Tests: протестировано локально
Relates: TAXI-3149, TAXI-3152
```

### Same guidelines in Russian:
https://wiki.yandex-team.ru/taxi/backend/userver/commit-message-guidelines/

### Rules

1. A commit message consists of three parts: first line, full description, tags. They are separated with blank lines.

2. Every line should be no more than 72 characters long. This restriction enhances readability of GitHub pages. This is mandatory for the first line and less strictly recommended for all other parts.

3. First line consists of three parts: type of commit, component and message.

4. Type of commit should be one of the following:
   - bug: this commit fixes some noticeable bug
   - fix: same as bug
   - typo: this commit fixes some trivial typo or minor bug that is not worth including in release changelog
   - feat: this commit introduces a new feature
   - cc: this commit fixes coding conventions or comments in code (pep8, etc.)
   - refactor: this commit significantly changes the code, but does not introduce any new functionality

5. Component is a part of service that is mostly affected by the change. Should be name of the service or one of the following:
   - admin
   - cabinet
   - client: client protocol
   - exams
   - park: taxi park protocol
   - docs
   - tasks: celery and cron tasks
   - core: affects several or all components

6. Message should describe essential meaning of changes in this commit. It should always fit a sentence like "Dmitry, please …" - for example, "Dmitry, please remove 'protocol' from logs". Never "removes", never "removed". You can also think about this as what this commit will do if applied. So you should be able to formulate the following sentence: "If applied, this commit would \<your commit message here\>".

7. List of types and components is subject to change during lifetime of the project.

8. For now, there is only two type of tags: 
    - "Relates". It indicates jira/startrek tasks that are related to this commit, for purposes of automatization. Note that this is different from usual "Closes" line: "Relates" does not imply that you actually closed some task with this commit - maybe just added some code to investigate the problem.
    - "Tests". You can describe your testing here. Description must be in Russian language. Without this tag **you have to describe your testing in related ticket!**

9. On doing Squash and Merge in Github interface please move first line into pull request header and preserve pull request id suffix (`(#127)`).