Blocking Commits
================
During approval, some commits can block other commits. There are several ways how a commit can block another one. These ways are described below.


Contributing Commits
--------------------
An object history is described by a chain of commits. We say that an earlier commit in the history **contributes** to a later one. In the example below, commit 1 contributes to commit 2:

    (1) <- 2

If commit 1 has an active moderation task then commit 2 cannot be approved and we say that commit 1 is blocking and commit 2 is blocked.


### Master-Slave Relations ###
Commits with a master-slave relation also contributes to each other.

In the example below, commit 1 with an active moderation task blocks commit 2 by means of master-slave relation.

    (1)
     | master-slave
     2


Commits Made by Service Tasks
-----------------------------
Service tasks may perform huge changes. Such big changes are split on several commits. All these commits must be approved simultaneously. If among these commits there is a commit blocked by a contributing commit then this commit by itself is blocking for all commits in this group of commits made by this service task.

In the example below, commits 2 and 3 has been made by a service task. The commit 2 is blocked on the commit 1 (that has an active moderation task). At the same time commit 3 is blocked on the commit 2.

    (1) <- 2
           |
           3


Logically Connected Commits
---------------------------
We say that two commits are **logically connected** if one of those commits might block another one directly or indirectly.


Approving Process
=================
Commits ready to be approved are pushed to the PreApproved queue. Only non-blocked commits are moved from the PreApproved queue to the Approved queue. Moreover, all logically connected commits are approved simultaneously.


Commits Relations
-----------------
Information about commits relations is stored in the DB to achieve simultaneous approving of logically connected commits. Information is stored in the table `revision_meta.preapproved_commits_relations` in the form of commit identities pairs.

If a commit contributes to another one then for such a pair an entry is added into the DB.

For commits made by a service task added `commits number - 1` relations. Each commit but the first one are connected to the first commit in the group.


Approving Algorithm
-------------------
The information about commits relations can be represented in form of a graph, where commits are placed in the vertexes and edges represents relations between connected commits.

This graph reflects logical connections between commits: two logically connected commits has a path connected them. Therefore, a graph component represents a group of logically connected commits that must be approved simultaneously. Commits from a component can be approved if all related moderation tasks are closed.

So, the approving algorithm consists of the following steps:
- load all relations from `preapproved_commits_relations` and commit identities from `preapproved_commits_queue` tables;
- build a graph;
- for each graph component:
  - approve all commits from the component if all related moderation tasks are closed.
