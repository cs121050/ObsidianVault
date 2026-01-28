

## delete all data from table
TRUNCATE TABLE videocontainsartist, video, artist, type RESTART IDENTITY CASCADE;


### How to save your parametric data of a table
To actually save the data as insert statements:
- Right-click the database → **Tasks → Generate Scripts…**
- Choose **“Select specific database objects”** → select only the tables with parametric data.
- Click **Next → Set Scripting Options → Advanced**.
- Set **Types of data to script = Data only**.
- Finish the wizard → you now have a `.sql` file with `INSERT` statements.
or do that 
```sql

--that created a backup table :D
SELECT *
INTO VideoContainsArtist_backup
FROM VideoContainsArtist;

INSERT INTO VideoContainsArtist
SELECT * FROM VideoContainsArtist_backup;