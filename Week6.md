# Normalization or Schema Refinement
- A technique of organizing the data in the database
- A systematic approach of decomposing tables to eliminate data redundancy and undesirable characteristics
- Most common technique for the Schema Refinement is decomposition.
- Normalization is used for mainly two purpose:
    - Eliminating redundant (useless) data
    - Ensuring data dependencies make sense, that is, data is logically stored

# Normal Forms
- A normal form specifies a set of conditions that the relational schema must satisfy in terms of its constraints – they offer varied levels of guarantee for the design
- Normalization rules are divided into various normal forms. Most common normal forms are:
  - **First Normal Form (1NF)**
  - **Second Normal Form (2NF)**
  - **Third Normal Form (3NF)**
- Additional Normal Forms:
    - Elementary Key Normal Form (EKNF) 
    - **Boyce-codd Normal Form (BCNF) **
    - **Multivalued Dependencies And Fourth Normal Form (4NF) **
    - Essential Tuple Normal Form (ETNF) 
    - Join Dependencies and Fifth Normal Form (5NF) 
    - Sixth Normal Form (6NF)
    - Domain/Key Normal Form (DKNF)

## 1NF: First Normal Form
- A relation is in First Normal Form if and only if all underlying domains contain atomic values only (doesn’t have multivalued attributes (MVA))

## 2NF: Second Normal Form
- Relation R is in Second Normal Form (2NF) only iff : 
    - R is in 1NF and
    - R contains no Partial Dependency

### Partial Dependency:
Let R be a relational Schema and X, Y, A be the attribute sets over R where X : Any Candidate Key, Y : Proper Subset of Candidate Key, and A : Non Prime Attribute 
    If Y → A exists in R, then R is not in 2NF.

(Y → A) is a Partial dependency only if 
- Y: Proper subset of Candidate Key 
- A: Non Prime Attribute

A *prime attribute* of a relation is an attribute that is a part of a candidate key of the relation

## 3NF: Third Normal Form
- A relational schema R is in 3NF if for every FD X → A associated with R either
    - A ⊆ X (that is, the FD is trivial) or 
    - X is a superkey of R or
    - A is part of some candidate key (not just superkey!)

- A relation in 3NF is naturally in 2NF and should not have a transitive dependency.

### Transitive Dependency
- A **transitive dependency** is a functional dependency which holds by virtue of transitivity. A transitive dependency can occur only in a relation that has three or more attributes.
- Let A, B, and C designate three distinct attributes (or distinct collections of attributes) in the relation. Suppose all three of the following conditions hold: 
    - A → B 
    - It is not the case that B → A (Does not hold)
    - B → C
- Then the functional dependency A → C (which follows from 1 and 3 by the axiom of transitivity) is a transitive dependency 

# Comparison of BCNF and 3NF
- It is always possible to decompose a relation into a set of relations that are in *3NF* such that: 
    - the decomposition is lossless
    - the dependencies are preserved

- It is always possible to decompose a relation into a set of relations that are in *BCNF* such that:
    - the decomposition is lossless 
    - it may not be possible to preserve dependencies

| S# | 3NF | BCNF |
| --- | --- | --- |
| 1. | It concentrates on Primary Key | It concentrates on Candidate Key |
| 2. | Redundancy is high as compared to BCNF | 0% redundancy |
| 3. | It preserves all the dependencies | It may not preserve the dependencies |
| 4. | A dependency X → Y is allowed in 3NF if X is a super key or Y is a part of some key | A dependency X → Y is allowed if X is a super key |

# MVD: Multivalued Dependency

Let R be a relation schema and let α ⊆ R and β ⊆ R. The multivalued dependency **α :fast_forward: β** holds on R if in any legal relation r(R), for all pairs for tuples t1 and t2 in r such that t1[α] = t2 [α], there exist tuples t3 and t4 in r such that:

    t1[α] = t2 [α] = t3 [α] = t4 [α] 
    t3[β] = t1 [β]
    t3[R – β] = t2[R – β]
    t4 [β] = t2[β]
    t4[R – β] = t1[R – β]

- We use multivalued dependencies in two ways: 
    - To test relations to determine whether they are legal under a given set of functional and multivalued dependencies
    - To specify constraints on the set of legal relations. We shall thus concern ourselves only with relations that satisfy a given set of functional and multivalued dependencies.
- If a relation r fails to satisfy a given multivalued dependency, we can construct a relations r’ that does satisfy the multivalued dependency by adding tuples to r.

|   | Name | Rule |
| --- | --- | --- |
| C- | Complementation | If X :fast_forward: Y, then X :fast_forward: (R − (X ∪ Y)) |
| A- | Augmentation | If X :fast_forward: Y and W ⊇ Z, then WX :fast_forward: YZ |
| T- | Transitivity | If X :fast_forward: Y and Y :fast_forward: Z, then X :fast_forward: (Z − Y) |
|  | Replication | If X → Y, then X :fast_forward: Y but the reverse is not true |
|  | Coalescence | If X :fast_forward: Y and there is a W such that W ∩ Y is empty, W→ Z and Y ⊇ Z, then X → Z |

- A MVD **X :fast_forward: Y** in **R** is called a trivial MVD if
    - **Y** is a subset of **X (X ⊇ Y)** or 
    - **X ∪ Y = R**. Otherwise, it is a non trivial MVD and we have to repeat values redundantly in the tuples.


# Temporal Databases

- Some data may be inherently historical because they include time-dependent / time-varying data, such as:
    - Medical Records 
    - Judicial records 
    - Share prices 
    - Exchange rates, etc.

- The desire to model such data means that we need to store not only the respective value but also an associated date or a time period for which the value is valid.
- Temporal databases provide a uniform and systematic way of dealing with historical data

## Temporal Data
- *Temporal data* have an association time interval during which the data are valid.
- A *snapshot* is the value of the data at a particular point in time

## Temporal Database Theory

- **Model of Temporal Domain**: Single-dimensional linearly ordered which may be 
    - Discrete or dense 
    - Bounded or unbounded 
    - Single dimensional or multi-dimensional
    - Linear or non-linear

- Timestamp Model 
- Temporal ER model by adding valid time to 
    - Attributes: address of an instructor at different points in time 
    - Entities: time duration when a student entity exists 
    - Relationships: time during which a student attended a course 
    - But no accepted standard
- Temporal Functional Dependency Theory 
- Temporal Logic 
- Temporal Query Languge: TQuel [1987], TSQL2 [1995], SQL/Temporal [1996], SQL/TP [1997]

## Modeling Temporal Data: Uni / Bi Temporal
- There are two different aspects of time in temporal databases
    - **Valid Time**: Time period during which a fact is true in real world, provided to the system.
    - **Transaction Time**: Time period during which a fact is stored in the database, based on transaction serialization order and is the timestamp generated automatically by the system.
 
 - Temporal Relation is one where each tuple has associated time; either valid time or transaction time or both associated with it. 
    - **Uni-Temporal Relations**: Has one axis of time, either Valid Time or Transaction Time.
    - **Bi-Temporal Relations**: Has both axis of time – Valid time and Transaction time. It includes Valid Start Time, Valid End Time, Transaction Start Time, Transaction
End Time.

## Modeling Temporal Data: Summary
- Advantages:
    - The main advantages of this bi-temporal relations is that it provides historical and roll back information. 
        - Historical Information – Valid Time.
        - Rollback Information – Transaction Time.

- Disadvantages:
    - More storage 
    - Complex query processing
    - Complex maintenance including backup and recovery
