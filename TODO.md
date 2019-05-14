# TODO

- [ ] Debug API/UI
- [ ] NEST
  - [ ] TypeScript
  - [ ] Auth/ JWT

Database

- [X] Name UNIQUE Index
- [ ] UNIQUE Relationship  


https://neo4j.com/docs/cypher-manual/current/schema/constraints/#constraints-create-unique-constraint

CREATE CONSTRAINT ON (u:User) ASSERT u.name IS UNIQUE
CREATE CONSTRAINT ON (b:Business) ASSERT b.name IS UNIQUE
CREATE CONSTRAINT ON (c:Category) ASSERT c.name IS UNIQUE
CALL db.constraints

https://neo4j.com/docs/cypher-manual/current/clauses/create-unique/#create-unique-create-labeled-node-if-missing

# create only one with MERGE
MATCH (u1:User {name: 'Kapa'})
MERGE (u2:User {name: 'Pelu'})
MERGE (u1)-[r1:FRIENDS]->(u2)
MERGE (u2)-[r2:FRIENDS]->(u1)
RETURN u1,u2

:params {from: 60, to: 48}
RETURN $from

:params
{
  "from": "u3",
  "to": "u4"
}

For clear params in neo4j-browser type :params {}.
For additional help type :help params.

MATCH (from:User {id: $from})
MATCH (to:User {id: $to})
MERGE (from)-[:FRIENDS]->(to)
RETURN from,to