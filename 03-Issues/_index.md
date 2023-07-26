# issues

```dataview
table 
	rows.file.link as "name",
	rows.status as status
from #issue
where status != "done"
sort file.name
group by type
```



