
```sql
``` ========== Base Search ========== ```
| index=bin source=street_devices sourcetype=text
| fields source sourcetype 
| where successes>0 AND failures>100
| timechart by host span=1h limit=10

``` ========== Final Table ========== ```
| table
```
