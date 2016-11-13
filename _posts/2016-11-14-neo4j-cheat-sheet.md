---
title: Neo4j Cheat sheet
---

## Neo4j

- Lists of key concepts from my experiences.
- Snippets for fast lookup.
- Based on [developer manual](https://neo4j.com/docs/developer-manual/current/)


## Firing Up

Fire up quickly with [Docker official image](https://hub.docker.com/r/library/neo4j/):

```bash
$ docker run --rm -it -p 7474:7474 --env=NEO4J_AUTH=none neo4j
```


## Nodes

- Nodes can have **one or more** labels.


## Relationships

- Unlike labels, relationships can only have **one type**.
- Every relationship has **a direction**.
- There are **no performance differences** related to directions.
- You can simply ignore them if you don't need them. 


## Properties

- Both nodes and relationships can have properties.
- `NULL` is not a valid property value.
- `NULL` can be modeled by the absence of a key.


## Uniqueness


```cypher
CREATE ({name: "Finn"}) -[:FRIEND]-> ({name: "Jake"}) -[:FRIEND]-> ({name: "Rainicorn"})
```

Let's find out friends of friends of *Finn*.

```cypher
MATCH (a) -[:FRIEND]- (b) -[:FRIEND]- (c)
WHERE a.name = "Finn"
RETURN c
```
*Angle brackets(`>`) are intentionally omitted for ignoring directions*


It returns only *Rainicorn* as expected.  
But from the theoretical perspective,
*Finn* himself is valid for variable `c`. But it's suppressed.

This is because Neo4j **doesn't use the same relationship multiple times within a single pattern**. 
You need to divide up MATCH clause to have *Finn* included:

```cypher
MATCH (a) -[:FRIEND]- (b)
MATCH (b) -[:FRIEND]- (c)
WHERE a.name = "Finn"
RETURN c
```


## Ordering NULL

- `NULL` will always come at the end of the result set for ascending sorting.


## MERGE vs CREATE UNIQUE

- `CREATE UNIQUE` has slightly more obscure semantics than `MERGE`.
- `CREATE UNIQUE` is *deprecated*. 

[Stack overflow](http://stackoverflow.com/questions/22773562/difference-between-merge-and-create-unique-in-neo4j)


## cycli

[cycli](https://github.com/nicolewhite/cycli) is a command-line interface for Neo4j.

```bash
$ pip install cycli
$ cycli -f FILENAME  (Execute semicolon-separated Cypher queries)
```


## Cheat sheet

### Basics

```cypher
(a:User)-->(b)
(a:User:Admin)-->(b)
(a { name: "Andres", sport: "Brazilian Ju-Jitsu" })
(a)-[{blocked: false}]->(b)
(a)--(b)
(a)-[r]->(b)
(a)-[r:REL_TYPE]->(b)
(a)-[r:TYPE1|TYPE2]->(b)
(a)-[:REL_TYPE]->(b)
(a)-[*2]->(b)
(a)-[*3..5]->(b)
(a)-[*3..]->(b)
(a)-[*..5]->(b)
(a)-[*]->(b)
(a)-[:REL_TYPE*1..2]->(b)
```

### CREATE, MERGE, DELETE

```cypher
CREATE (n:Person { name : 'Andres', title : 'Developer' })

MATCH (a:Person),(b:Person)
WHERE a.name = 'Node A' AND b.name = 'Node B'
CREATE (a)-[r:RELTYPE]->(b)
RETURN r

// MATCH or CREATE if not exists
MERGE (charlie { name:'Charlie Sheen', age:10 })
RETURN charlie

// Either everything matches or everything is created
MATCH (oliver:Person { name:'Oliver Stone' }),(reiner:Person { name:'Rob Reiner' })
MERGE (oliver)-[:DIRECTED]->(movie:Movie)<-[:ACTED_IN]-(reiner)
RETURN movie

MATCH (person:Person)
MERGE (city:City { name: person.bornIn })
MERGE (person)-[r:BORN_IN]->(city)
RETURN person.name, person.bornIn, city

MATCH (n:Useless)
DELETE n

// Delete all notes and relationships
MATCH (n)
DETACH DELETE n

```


### SET, REMOVE, FOREACH

```cypher
MATCH (n { name: 'Andres' })
SET n.surname = 'Taylor'
RETURN n

// equivalent to REMOVE
MATCH (n { name: 'Andres' })
SET n.name = NULL RETURN n

MATCH p =(begin)-[*]->(END )
WHERE begin.name='A' AND END .name='D'
FOREACH (n IN nodes(p)| SET n.marked = TRUE )
```


### Indexes and constraints

```cypher
CREATE INDEX ON :Person(name)

MATCH (person:Person { name: 'Andres' })
RETURN person

DROP INDEX ON :Person(name)

CREATE CONSTRAINT ON (n:Person) ASSERT n.name IS UNIQUE;
```

### WHERE

```cypher
WHERE n:Swedish
WHERE exists(n.belt)
WHERE person.belt IS NULL
WHERE n.name STARTS WITH 'Pet'
WHERE n.name ENDS WITH 'ter'
WHERE n.name CONTAINS 'ete'
WHERE NOT n.name ENDS WITH 's'
WHERE n.name =~ 'Tob.*'
WHERE n.address =~ 'Sweden\\/Malmo'
WHERE n.name =~ '(?i)ANDR.*'

MATCH (tobias { name: 'Tobias' }),(others)
WHERE others.name IN ['Andres', 'Peter'] AND (tobias)<--(others)
RETURN others

WHERE (n)-[:KNOWS]-({ name:'Tobias' })
WHERE n.name='Andres' AND type(r)=~ 'K.*'
```


### SKIP, LIMIT

```cypher
// Return middle two
MATCH (n)
RETURN n
ORDER BY n.name
SKIP 1
LIMIT 2
```


### Others

```cypher
MATCH (me:Person)-->(friend:Person)-->(friend_of_friend:Person)
WHERE me.name = 'A'
RETURN count(DISTINCT friend_of_friend), count(friend_of_friend)

MATCH (david { name: "David" })--(otherPerson)-->()
WITH otherPerson, count(*) AS foaf
WHERE foaf > 1
RETURN otherPerson

UNWIND[1,2,3] AS x
RETURN x

WITH [1,1,2,2] AS coll UNWIND coll AS x
WITH DISTINCT x
RETURN collect(x) AS SET

MATCH (n:Actor)
RETURN n.name AS name
UNION ALL MATCH (n:Movie)
RETURN n.title AS name

```


## Links
- [Functions](https://neo4j.com/docs/developer-manual/current/cypher/#query-function)
- [Neo4j Documentation](http://neo4j.com/docs/)
- [Neo4j Bolt Driver for Python](https://neo4j.com/docs/api/python-driver/current/)
