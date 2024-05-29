
```sql
``` ========== Base Search ========== ```
| index=bin source=street_devices sourcetype=text
| fields source sourcetype
| eval eval_test=if(type=1, "1", "0")
| where successes>0 AND failures>100
| timechart by host span=1h limit=10

``` ========== Final Table ========== ```
| table
```
