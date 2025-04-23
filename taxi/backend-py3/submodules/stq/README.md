# Sharded tasks queue

## The big picture

Clients put tasks into queue. Workers take tasks, execute and mark as
done or failed.

To put task into queue client calculates shard (which is a database) and
saves task metadata into queue.

Worker takes tasks from one or more shards. When it takes task it locks
task on itself and updates entry in database with heartbeats while task
is executed. When task execution is finished result is saved into
database.


    Clients:    client1  client2  ...  clientN
                  |
                  + ------+--- ...  ----+
                  |       |             |
                  V       V             V
    Databases:  shard0  shard1  ...  shardN-1
                   ^ \ /            /
                   |  X          +-+
                   | / \        /
                   |/   \      /
    Workers:    worker1  worker2  ...  workerN


## How to start

Please, see example in `benchmark/blocking_pymongo`.


## Development process

Please, send pull requests to develop.

There is gitflow with following settings:

    [gitflow "branch"]
        master = master
        develop = develop
    [gitflow "prefix"]
        feature = feature/
        release = release/
        hotfix = hotfix/
        support = support/
        versiontag = 
    [gitflow "path"]
        hooks = .git/hooks
