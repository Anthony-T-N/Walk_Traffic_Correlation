
```sql
``` ========== Base Search ========== ```
| index=bin source=street_devices sourcetype=text
| where successes>0 AND failures>100
| timechart by host span=1h 

``` ========== Final Table ========== ```
| table
```
