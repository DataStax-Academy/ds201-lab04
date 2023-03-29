<!-- TOP -->
<div class="top">
  <img class="scenario-academy-logo" src="https://datastax-academy.github.io/katapod-shared-assets/images/ds-academy-2023.svg" />
  <div class="scenario-title-section">
    <span class="scenario-title">Clustering Columns</span>
    <span class="scenario-subtitle">ℹ️ For technical support, please contact us via <a href="mailto:academy@datastax.com">email</a>.</span>
  </div>
</div>

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 1 of 2</span>
 <a href='command:katapod.loadPage?[{"step":"step3"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Explore the <i>videos_by_tag</i> table</div>

Clustering columns are the columns that are part of the primary key, but are not part of the partition key. This exercise will help you understand how clustering columns affects queries and how you can filter rows with them.

Use `nodetool` to verify that Cassandra is running. (You may need to run this command multiple times.)

✅ Verify that Cassandra is running.
```
apache-cassandra-4.1.0/bin/nodetool status
```

✅ Start 'cqlsh' so you can execute CQL statements:
```
apache-cassandra-4.1.0/bin/cqlsh
```

✅ Switch to the *killrvideo* keyspace via the `USE` command:
```
USE killrvideo;
```

✅ Execute the following command to view information about the *videos* table: 
```
DESCRIBE TABLE videos_by_tag;
```

You should see the following table definition

`CREATE TABLE killrvideo.videos_by_tag (`<br>
&nbsp;&nbsp;&nbsp;&nbsp;`tag text,`<br>
&nbsp;&nbsp;&nbsp;&nbsp;`video_id timeuuid,`<br>
&nbsp;&nbsp;&nbsp;&nbsp;`title text,`<br>
&nbsp;&nbsp;&nbsp;&nbsp;`PRIMARY KEY (tag, video_id)`<br>
`) ...`

In this table the prartition key is `tag` and the clustering column is `video_id`. Therefore, rows are grouped by `tag` and ordered by `video_id`.

Clustering columns support both equality and inequality predicates for CQL queries and also allow ordering within a partition. Define and execute several CQL queries against table videos_by_tag that use equality (=) and inequality (>,>=,<,<=) predicates, as well as row ordering with the ORDER BY clause.

✅ Select *all* videos:
```
SELECT * FROM videos_by_tag;
```

✅ Select a specific partition:
```
SELECT * FROM videos_by_tag
WHERE tag = 'cassandra';
```

✅ Select a specific video:
```
SELECT * FROM videos_by_tag
WHERE tag = 'cassandra' AND
      video_id =  245e8024-14bd-11e5-9743-8238356b7e32;
```

✅ Select videos using an inequality:
```
SELECT * FROM videos_by_tag
WHERE tag = 'cassandra' AND
      video_id <= 245e8024-14bd-11e5-9743-8238356b7e32;
```

✅ Select videos using an inequality and reverse the order:
```
SELECT * FROM videos_by_tag
WHERE tag = 'cassandra' AND
      video_id <= 245e8024-14bd-11e5-9743-8238356b7e32
ORDER BY video_id DESC;
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step2"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>
