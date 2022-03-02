## Features of a Good Relational Design
- Reflects real-world structure of the problem 
- Can represent all expected data over time 
- Avoids redundant storage of data items 
- Provides efficient access to data 
- Supports the maintenance of data integrity over time 
- Clean, consistent, and easy to understand


## Redundancy
    Having multiple copies of same data in the database.

- This problem arises when a database is not normalized
- It leads to anomalies


## Anomaly
    Inconsistencies that can arise due to data changes in a database with insertion, deletion, and update
    
- These problems occur in poorly planned, un-normalised databases where all the data is stored in one table (a flat-file database)
- There can be three kinds of anomalies:
  1. **Insertions Anomaly** - When the insertion of a data record is not possible without adding some additional unrelated data to the record
  2. **Deletion Anomaly** - When deletion of a data record results in losing some unrelated information that was stored as part of the record that was deleted from a table
  3. **Update Anomaly** - When a data is changed, which could involve many records having to be changed, leading to the possibility of some changes being made incorrectly


`Dependency ⇒ Redundancy ⇒ Anomaly`

`Normalization ⇒ Good Decomposition ⇒ Minimization of Dependency ⇒ Min Dependency ⇒ Min Redundancy ⇒ Min Anomaly`