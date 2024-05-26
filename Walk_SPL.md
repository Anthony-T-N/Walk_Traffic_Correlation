
```sql
``` ========== Base Search ========== ```
| index=bin source=street_devices sourcetype=text
| where successes>0 AND failures>100

``` ========== Final Table ========== ```
| table
```
