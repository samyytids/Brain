---
tags:
  - area
Links:
  - "[[Programming]]"
---
## Projects
### Not started
```dataview
table Status, Deadline
from [[]] AND #project 
where contains(Status, "Not started")
sort Deadline asc
```
### In progress
```dataview
table Status, Deadline
from [[]] AND #project 
where contains(Status, "In progress")
sort Deadline asc
```
### Finished
```dataview
table Status, Deadline
from [[]] AND #project 
where contains(Status, "Finished")
sort Deadline asc
```
