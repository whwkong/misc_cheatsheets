# sqlite3 Cheatsheet

Notes on using sqlite to query db

Common display modes (modes can be set in `~/.sqliterc`)

```
    > -- comments can be double-dashes or /* C-style comments */
    > .headers on                   -- turn on column headers for select
                                    -- statements; very useful 
    > .mode list                    -- default mode; useful for piping to awk 
    > .mode column                  -- most useful display mode
```

```
    $ sqlite duties_schedule.db
    > 
    > .tables
    > select * from duty
    > select * from member
    > select * from member where training=True
    > .exit
    
    
    > pragma table_info(member);    -- lists all columns in member
    > .schema                       -- shows schema of db
    > .schema <table>               -- shows schema of table
```




sqlite3 commands
```
    .help
    .exit 
```


