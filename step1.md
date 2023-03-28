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

<div class="step-title">Explore the videos_by_tag table</div>

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
✅ Do something
```
echo "something!"
```

✅ Do something else
```
echo "something else!"
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
