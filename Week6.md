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


