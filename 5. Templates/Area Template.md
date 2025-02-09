---
tags:
  - area
Links:
---
## Projects
### Not started
```dataview
table Status, Deadline
from [[]] AND #project 
where contains(Status, "Not started")
```
### In progress
```dataview
table Status, Deadline
from [[]] AND #project 
where contains(Status, "In progress")
```
### Completed
```dataview
table Status, Deadline
from [[]] AND #project 
where contains(Status, "Completed")
```
