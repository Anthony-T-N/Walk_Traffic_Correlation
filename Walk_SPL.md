
```sql
``` ========== Base Search ========== ```
| multisearch
  [search index=bin source=street_devices sourcetype=frames earliest=-1d@d latest=now()]
  [search index=bin2 source=highway_devices sourcetype=frames earliest=-1d@d latest=now()]
  [search index=bin3 source=forest_devices sourcetype=frames earliest=-1d@d latest=now()]
| fields source sourcetype
``` ========== Comparison ========== ```
| lookup target_list.csv person_ID OUTPUT section walking_style
``` ========== Cleaning Logic ========== ```
| eval eval_test=if(type=1, "1", "0")
| eval individual = coalesce(person, character, being)
| where suspected_age>21 AND suspected_age<40
| stats max(suspected_age) AS max_age_in_range
``` ========== Coordinate Extraction ========== ```
| iplocation current_phone_ip
| geostats latfield=lat_cords longfield=long_cords
| timechart count by host span=1h limit=10
```

```sql
``` ========== Base Search ========== ```
index=bin source=street_devices sourcetype=frames earliest=-1mon@mon latest=-5d@d+5m+40s
``` Whitelist ```
NOT [| inputlookup whitelist.csv | fields source sourcetype individual]
[search index=bin2 source=street_devices sourcetype=frames individual!=A* | fields individual]
``` ========== Cleaning Logic ========== ```
```  individual_1, individual_2, individual_3 ```
| rename indvidual* AS person*

| eval fixed_time = relative_time(now(), "-1d@d")
| eval epoch_time = strptime(fixed_time, "Y-%m-%d %H:%M:%S,%N:")
``` ========== Final Table ========== ```
| table fixed_time epoch_time
```

