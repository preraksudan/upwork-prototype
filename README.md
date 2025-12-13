##  Table 1 (main):
```
id (primary key)
text1 (varchar 255) [audio]
text2 (varchar 255) [tag name]
```

```sql
-- Table 1: main
  CREATE TABLE main (
      id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
      text1 VARCHAR(255) NOT NULL,
      text2 VARCHAR(255) NOT NULL
  );
```


## Table 2 (tag_definitions):

```
tag_name (varchar 64) - primary key
tag_description (varchar 128)
```

```sql
  -- Table 2: tag_definitions
  CREATE TABLE tag_definitions (
      tag_name VARCHAR(64) PRIMARY KEY,
      tag_description VARCHAR(128) NOT NULL
  );
```


##  Table 3 (main_tags)

```
fk_table_1_id (primary key)  -- linked to table 1
fk_table_2_tag_name (primary key)  -- linked to table 2
```

```sql
-- Table 3: main_tags (many-to-many mapping)
CREATE TABLE main_tags (
    fk_table_1_id INT UNSIGNED NOT NULL,
    fk_table_2_tag_name VARCHAR(64) NOT NULL,

    PRIMARY KEY (fk_table_1_id, fk_table_2_tag_name),

    CONSTRAINT fk_main_tags_main
        FOREIGN KEY (fk_table_1_id)
        REFERENCES main(id)
        ON DELETE CASCADE,

    CONSTRAINT fk_main_tags_tag
        FOREIGN KEY (fk_table_2_tag_name)
        REFERENCES tag_definitions(tag_name)
        ON DELETE CASCADE
) ENGINE=InnoDB;
```



## Table 4 (main_audio) -- linked to table 1

```
fk_table_1_id  (unsigned int, primary key)
audio_name (varchar 255, primary key)
```

```sql
-- Table 4: main_audio
  CREATE TABLE main_audio (
      fk_table_1_id INT UNSIGNED NOT NULL,
      audio_name VARCHAR(255) NOT NULL,

      PRIMARY KEY (fk_table_1_id, audio_name),

      CONSTRAINT fk_main_audio_main
          FOREIGN KEY (fk_table_1_id)
          REFERENCES main(id)
          ON DELETE CASCADE
  ) ENGINE=InnoDB;
```
---
Each entry will be displayed in HTML as:

Entry ID, Text 1, Text 2
- zero or more tags (that can be deleted or added to) - tags should appear as tag description. When a new tag is added, the list of available tag descriptions will be shown to choose from.
- zero or more audio files (that can be deleted or added to) (added audio files are uploaded to the server)

#### Few Clarifying Questions (related to data source and management)
```questions
- Are audio files also stored as BLOB in Mysql DB.
- For each audio file is there a corresponding label and mapped description ?
- Is functionality for CRUD of tags and tag descrption also required.
- Can one audio have multiple tags associated to it ?
```
