---
tags:
  - note
Project:
  - "[[Learn BEAM VM]]"
Status: In progress
---
# Processes
You can think of these as being analogous to OS processes. They have their own private memory, a stack, a heap and a mailbox. 
Memory is not shared between Erlang processes, they communicate only through messages and signals.
A single Erlang node can have any processes and processes can communicate between nodes. 
# Scheduling
Effectively how Erlang is effortlessly concurrent.
This chooses which process to execute, it manages two queues
- Ready 
- Waiting
The BEAM VM takes a process off the top of its ready queue, runs it for a `time slice`. Once that slice is up if it is not blocking it is put at the bottom of the ready queue while if it is being blocked (awaiting a message) the process will be put into the waiting queue. 
Processes are only moved from the waiting queue to the ready queue once they have received whatever it is that they are waiting for.

There exists a scheduler per thread and these are spawned by default. 

Schedulers can take processes from another schedulers ready queue if they have run out of ready processes.

# Erlang tag scheme
Erlang is not a typed language, but it needs a way to keep track of types of data objects. This is achieved through tagging.
Effectively, part of the pointer/raw data is used to encode what type the data is which is used for pattern matching as well as for stuff like basic operators. I guess it kinda works like packstream does.

# Memory handling
Erlang is garbage collected, the stack and heap do not have a maximum size. They are initialized as being very small which is why the BEAM VM can host so many processes. The stack and heap are expanded and contracted based on the actual memory requirements of the process. 

Before the heap/stack are expanded the VM will initially check if there is anything that can be removed to allow for the new memory requirements. While this is being checked the memory is copied to a temporary version. If the GC can't free up enough space then a new heap/stack is allocated at the size that is required and then the data is moved to that. 

