<!-- TOP -->
<div class="top">
  <img class="scenario-academy-logo" src="https://datastax-academy.github.io/katapod-shared-assets/images/ds-academy-2023.svg" />
  <div class="scenario-title-section">
    <span class="scenario-title">Clustering Columns</span>
    <span class="scenario-subtitle">ℹ️ For technical support, please contact us via <a href="mailto:academy@datastax.com">email</a>.</span>
  </div>
</div>

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step1"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
<span class="step-count"> Step 2 of 2</span>
<a href='command:katapod.loadPage?[{"step":"finish"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Create the <i>latest_videos_by_tag</i> table.</div>

In this portion of the exercise, you will create a table that supports queries like this one.

`SELECT tag, video_id, added_date, title`<br>
&nbsp;&nbsp;&nbsp;&nbsp;`FROM latest_videos_by_tag`<br>
&nbsp;&nbsp;&nbsp;&nbsp;`WHERE tag = 'cassandra'`<br>
&nbsp;&nbsp;&nbsp;&nbsp;`ORDER BY added_date DESC;`

Rows will be grouped by *tag* and ordered by *added_date*. You will need to use *video_id* as part of the primary key to ensure uniqueness.

✅ Create the table:
```
CREATE TABLE latest_videos_by_tag (
  tag TEXT,
  video_id TIMEUUID,
  added_date TIMESTAMP,
  title TEXT,
  PRIMARY KEY ((tag), added_date, video_id)
) WITH CLUSTERING ORDER BY (added_date DESC, video_id ASC);
```

✅ Import `videos-by-tag.csv` into the new table:
```
COPY latest_videos_by_tag(tag, video_id, added_date, title)
FROM '/workspace/ds201-lab04/data-files/videos-by-tag.csv'
WITH HEADER = TRUE;
```

✅ Retrieve all the rowa from *latest_videos_by_tag*:

<details class="katapod-details">
  <summary>Solution</summary>

```
SELECT * FROM latest_videos_by_tag;
```

</details>
<br>

Verify that you get 4 rows as expected.

The rows should be grouped by a tag and, within each partition, ordered in descending order of an added date.

✅ Execute the original CQL query that table latest_videos_by_tag was designed for:
```
SELECT tag, video_id, added_date, title
FROM latest_videos_by_tag
WHERE tag = 'cassandra'
ORDER BY added_date DESC;
```

✅ Change the original query below to return the cassandra videos added after 2013-02-01:
```
SELECT tag, video_id, added_date, title
FROM latest_videos_by_tag
WHERE tag = 'cassandra' AND
      added_date > '2013-02-01'
ORDER BY added_date DESC;
```

✅ Change the original query below to return the oldest cassandra video from the table. Use `LIMIT 1` to return only the first video in a result set:
```
SELECT tag, video_id, added_date, title
FROM latest_videos_by_tag
WHERE tag = 'cassandra'
ORDER BY added_date ASC
LIMIT 1;
```
<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step1"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"finish"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>