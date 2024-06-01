
```sql
``` ========== Base Search ========== ```
| index=bin source=street_devices sourcetype=frames earliest=-1d@d latest=now()
| fields source sourcetype
``` ========== Cleaning Logic ========== ```
| eval eval_test=if(type=1, "1", "0")
| where suspected_age>21 AND suspected_age<40
``` ========== Coordinate Extraction ========== ```
| iplocation current_phone_ip
| timechart by host span=1h limit=10

``` ========== Final Table ========== ```
| table
```
