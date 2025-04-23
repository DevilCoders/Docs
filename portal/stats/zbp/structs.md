# Structures used

## bugs_dict

```
dict{
    date<str(yyyy-mm-dd)>: dict{
        stage<str( Development | Beta | Release | Testing | Production | Unlnown ): dict{
            resolution<str( won'tFix | willNotFix | fixed | opened )>: dict{
                # '_tasks': list<str(issue.key)>
                # '_tasks_crashid': dict{
                #     issue.key<str>: int | 0
                # }
                '_internal': dict{
                    'storyPoints': float | 0
                    'testingStoryPoints': float | 0
                    'crash_effect': int | 0
                    'crush_weight': int | 0
                }
                '_sla': {
                    issue.crashId<str( 1 | 2 | 10 | 100 | 1000 )>: dict{
                        violation_status<str( NOT_VIOLATED | WARN_CONDITIONS_VIOLATED | FAIL_CONDITIONS_VIOLATED )>: dict{
                            issue.key<str>: int(defualt=1)      # set?
                        }
                    }
                }
                priority<str( blocker | critical | normal | minor | trivial )>: int | 0
            }
        }
    }
}
```

## tasks_dict

```
dict{
    date<str(yyyy-mm-dd)>: dict{
        '_tasks': list<str(issue.key)>,
        '_internal': {
            'storyPoints': float | 0,
            'testingStoryPoints': float | 0
        }
        priority<str( blocker | critical | normal | minor | trivial )>: int | 0
    }
}
```

## date_items

```
dict{
    stage<str( _total_ | Development | Beta | Release | Testing | Production | Unknown | Other ): dict{
        resolution<str( Won't Fix | Fixed | Unresolved | Other )>: dict{
            'date': str('yyyy-mm-dd')
            'project': str
            'stage': str( _total_ | Development | Beta | Release | Testing | Production | Unknown | Other )
            'resolution': str( Won't Fix | Fixed | Opened | Other )
            'bugs_weight': int | 0
            'bugs_crush_effect': int | 0
            'bugs_crush_weight': int | 0
            'bugs_sp': float | 0
            'bugs_tsp': float | 0
            'bug_blocker': int | 0
            'bug_critical': int | 0
            'bug_normal': int | 0
            'bug_minor_trivial': int | 0
            'tasks_weight': int | 0
            'tasks_sp': float | 0
            'tasks_tsp': float | 0
            'task_blocker': int | 0
            'task_critical': int | 0
            'task_normal': int | 0
            'task_minor_trivial': int | 0
        }
    }
}
