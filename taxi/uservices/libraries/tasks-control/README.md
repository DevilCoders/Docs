# Tasks control

This small library provides classes that help manage number of simultaneously
executing tasks. Real-world use case: say you receive a large data payload and
for each such payload you move it into coroutine and launches it. If, for some
reason or another your coroutine is slow and you receive more payloads per
second that you can process, number of coroutines will quickly increase. As each
coroutine stores payload inside it, you will quickly run out of memory and hello
OOM.

Library provides following classes:
1. tasks_control::DeposingTasksControl. Set a number - say 10 and if you attempt to launch
   11th coroutine, it will kill the oldest one. On a basis that it is probably
   less required.
2. tasks_control::PayloadQueue. Push an args for callback invocation into the
   queue and it will attempt to process them as fast as possible, using
   specified limits. Everything that can't be processed will be discarded.
   Essentially this is ad-hoc surge-protection for any message bus

