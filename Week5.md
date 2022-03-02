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
  1. **_Insertion Anomaly_** - When the insertion of a data record is not possible without adding some additional unrelated data to the record
  2. **_Deletion Anomaly_** - When deletion of a data record results in losing some unrelated information that was stored as part of the record that was deleted from a table
  3. **_Update Anomaly_** - When a data is changed, which could involve many records having to be changed, leading to the possibility of some changes being made incorrectly


`Dependency ⇒ Redundancy ⇒ Anomaly`

`Normalization ⇒ Good Decomposition ⇒ Minimization of Dependency ⇒ Min Dependency ⇒ Min Redundancy ⇒ Min Anomaly`


## Functional Dependencies 
A functional dependency is a constraint that specifies the relationship between two sets of attributes where one set can accurately determine the value of other sets. 
It is denoted as X → Y, where X is a set of attributes that is capable of determining the value of Y.

### Armstrong’s Axioms
Given a set of Functional Dependencies F, we can infer new dependencies by the Armstrong’s Axioms: 
- Reflexivity: if β ⊆ α, then α → β 
- Augmentation: if α → β, then γα → γβ
- Transitivity: if α → β and β → γ, then α → γ
    
### Armstrong’s Axioms: Derived Rules
- Union: if α → β holds and α → γ holds, then α → βγ holds 
- Decomposition: if α → βγ holds, then α → β holds and α → γ holds
- Pseudotransitivity: if α → β holds and γβ → δ holds, then αγ → δ holds

### Closure of Attribute Sets
Given a set of attributes α, define the closure of α under F (denoted by α+) as the set of attributes that are functionally determined by α under F.

Algorithm to compute α+, the closure of α under F:

    result ← α 
    while (changes to result) do 
        for each β → γ in F do 
            begin
                if β ⊆ result then result ← result ∪ γ
            end

#### Example:

R = (A, B, C, G, H, I)

F = {A → B, A → C, CG → H, CG → I, B → H} 

To complute _(AG)+_ 
- result = AG 
- result = ABCG (A → C and A → B) 
- result = ABCGH (CG → H and CG ⊆ AGBC)
- **result = ABCGHI** (CG → I and CG ⊆ AGBCH)

#### Uses:

There are several uses of the attribute closure algorithm:
- Testing for superkey:
    - To test if α is a superkey, we compute α+, and check if α+ contains all attributes of R.
- Testing functional dependencies
    - To check if a functional dependency α → β holds (or, in other words, is in F+), just check if β ⊆ α+
    - That is, we compute α+ by using attribute closure, and then check if it contains β.
    - Is a simple and cheap test, and very useful
- Computing closure of F
    - For each γ ⊆ R, we find the closure γ+, and for each S ⊆ γ+, we output a functional dependency γ → S.


