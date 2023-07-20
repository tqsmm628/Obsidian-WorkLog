```dataview
table 
	rows.file.link AS "Name"
from #issue
sort file.name
group by type
```
