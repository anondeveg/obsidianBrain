---
tags:
  - opensource
  - GSOC2026
  - round1
---


generated header files are compiled idl files!


event loop


## libuv design

In event-driven programming, an application expresses interest in certain events and respond to them when they occur. The responsibility of gathering events from the operating system or monitoring other sources of events is handled by libuv, and the user can register callbacks to be invoked when an event occurs. The event-loop usually keeps running foreveti a
![[Pasted image 20260117152101.png]]


event loop

**MULTI-THREADING IS NOT A MAGIC SOLUTIONS**

managing thousands of threads leads to high memory usage and higher chances of race conditions + worse performance due to resources being given to handling threads instead of processing it.

**Polling** = repeatedly asking the OS:
“Did anything happen yet?”

libuv uses os-level event pollers where it basiaclly says
hey os when x thing happen(event) wake me up! instead of constently asking the os "is my thing done yet???"
so the polling happens on the kernel level not the process

when does an event become 'ready'?
For a socket:

Readable → data available

Writable → send buffer has space

Hangup / errors

one event loop per thread (single threaded model)
**its not thread safe!**
![[Pasted image 20260117152644.png]]

If the loop is alive an iteration is started, otherwise the loop will exit immediately. So, when is a loop considered to be alive? If a loop has active and ref’d handles, active requests or closing handles it’s considered to be alive.

handles
requests
