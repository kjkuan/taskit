# Taskit
Taskit is a task runner written in Bash that is similar, in spirit, to other
tools such as *rake*, *fabric*, or *gulp*.  It lets you define tasks as
functions, with declared parameters and other attributes, in a `Taskfile, and
run them.  Task dependencies can be declared, and it dumps a stack trace on
execution errors. The goal is to provide a uniform interface for discovering
and running tasks defined in Bash.

> **NOTE**:
    Taskit shares many ideas described in this well explained [blog post],
    and takes a step further with its implementation to provide a better
    experience out of box.

[blog post]: https://hackernoon.com/introducing-the-taskfile-5ddfe7ed83bd#.ni9rl6fjt

# Taskfile
With the example [Taskfile](./Taskfile), running `taskit` from the same directory,
we can:

### See what options are available:

    $ taskit -h
    Usage: taskit [options] [task1 [name1=value1 ...] task2 ...]
    options:
      -h [TASK]    Show this help or a task specific help if a task is specified.
      -t           List all available tasks.
      -D           Skip task dependencies.
      -d           Dry run; show but don't really run any tasks.
      -x PATTERNS  Don't run any tasks matching the list of space-separated PATTERNS.
      -v LEVEL     Set the log verbosity level to LEVEL(error|warning|fatal|silence|info|debug).
      -f FILE      Use FILE as the Taskfile.

### Show available tasks:

    $ taskit -t
    Available tasks:

      mytask    -    A simple task

> **Note**:
    Taskit will list the tasks in the order they are defined in the Taskfile.
    This also takes into account tasks sourced from other files.

### See more detailed doc on a task:

    $ taskit -h mytask
    TASK
            mytask -- A simple task.

    DESCRIPTION
            Comments right before the task will be parsed as the task's
            help doc.


    PARAMETERS
            name!       Your name.
            greeting    Words to greet with.
            rest%       Rest of named arguments collected in an array.

### Run one or more tasks from CLI:

    $ taskit hello mytask name=Jack a=1 b=2
    71421115 SABERTOOTH|2017-03-04T15:20:25-0500|user=jkuan|pid=4150|INFO|Task::hello --
    hello world
    71421115 SABERTOOTH|2017-03-04T15:20:25-0500|user=jkuan|pid=4150|INFO|Task::count-from-one --
    1
    2
    3
    71421115 SABERTOOTH|2017-03-04T15:20:25-0500|user=jkuan|pid=4150|INFO|Task::count-from-one --
    1
    2
    3
    4
    5
    71421115 SABERTOOTH|2017-03-04T15:20:25-0500|user=jkuan|pid=4150|INFO|Task::mytask -- A simple task
    Hello, Jack
    The rest of named arguments are:
    a=1
    b=2
    71421115 SABERTOOTH|2017-03-04T15:20:26-0500|user=jkuan|pid=4150|INFO|Duration: 00:00:01


## Roadmap
Taskit is still a work in progress; things might change or get added, bugs are inevitable.
In particular, some areas still need to be improved:

  - current log/output format
    - the current format is not ideal, if you have any suggestions on how to best
      present task execution info/logs, please let me know.
    - we should also think about how to display info for remote tasks

  - properly document the public interface(i.e., global vars and functions, e.g., `taskit_run`)
    made available by taskit for use in a Taskfile.

Planned features:
  - remote tasks via ssh (WIP)
  - ability to run ansible modules

Bug report and suggestions via github issues, and PRs are welcomed!
