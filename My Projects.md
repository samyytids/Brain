## By Deadline
```dataview
table Status, Deadline, Area
from #project AND !"5. Templates" 
where Status != "Finished"
sort Deadline asc
```
