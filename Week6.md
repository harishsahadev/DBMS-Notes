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
  - **First Normal Form (1NF) **
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
