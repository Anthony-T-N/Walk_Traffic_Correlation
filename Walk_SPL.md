
```sql
``` ========== Base Search ========== ```
| multisearch
  [search index=bin source=street_devices sourcetype=frames earliest=-1d@d latest=now()]
  [search index=bin2 source=highway_devices sourcetype=frames earliest=-1d@d latest=now()]
| fields source sourcetype
``` ========== Comparison ========== ```
| lookup target_list.csv person_ID OUTPUT section walking_style
``` ========== Cleaning Logic ========== ```
| eval eval_test=if(type=1, "1", "0")
| where suspected_age>21 AND suspected_age<40
``` ========== Coordinate Extraction ========== ```
| iplocation current_phone_ip
| geostats latfield=lat_cords longfield=long_cords
| timechart by host span=1h limit=10
``` ========== Final Table ========== ```
| table
```
