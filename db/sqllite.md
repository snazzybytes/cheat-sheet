# SQLITE3 COMMANDS

### Open db file:
```
sqlite3 database_file.db
```

### Show all tables:

```sql
sqlite> .tables
event   tag   user_verification
```

### List all databases and their associated files:
```sql
sqlite> .databases
main: /embassy-data/package-data/volumes/nostr/data/main/nostr.db r/w
```

### Show schema of all tables:
```sql
sqlite> .schema
```

### Show schema of a table:
```sql
sqlite> .schema event

CREATE TABLE tag (
id INTEGER PRIMARY KEY,
event_id INTEGER NOT NULL, -- an event ID that contains a tag.
name TEXT, -- the tag name ("p", "e", whatever)
value TEXT, -- the tag value, if not hex.
value_hex BLOB, -- the tag value, if it can be interpreted as a lowercase hex string.
FOREIGN KEY(event_id) REFERENCES event(id) ON UPDATE CASCADE ON DELETE CASCADE
);
CREATE INDEX tag_val_index ON tag(value);
CREATE INDEX tag_val_hex_index ON tag(value_hex);
CREATE INDEX tag_composite_index ON tag(event_id,name,value_hex,value);
CREATE INDEX tag_name_eid_index ON tag(name,event_id,value_hex);
```
> NOTE: Must include ";" at the end of queries
### Show contents of a table:
```sql
sqlite> select * from event;

...or...

sqlite> select id, content, created_at, datetime(created_at,'unixepoch') from event where created_at > 1673579350 order by created_at desc limit 1;
```

### Insert a row in a table:
```sql
sqlite> INSERT INTO VARS (name,value) VALUES('color', 'blue');
```

### Insert or update (based on UNIQUE or PRIMARY KEY constraint):
```sql
sqlite> INSERT OR REPLACE INTO VARS (name,value) VALUES('color', 'blue');
```

### Delete a table:
```sql
sqlite> drop table ticket;
```

### Show execution time of a query:
```sql
sqlite> .timer ON
or
sqlite> .timer OFF

#
sqlite> select * from event;
...
Run Time: real 0.326 user 0.000523 sys 0.000261
```
