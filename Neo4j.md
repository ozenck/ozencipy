# **`Neo4j Notes`** 

[Udemy Course Link](https://htrdc.udemy.com/course/neo4j-foundations/learn/lecture/5160978#overview)

db.schema.visualization() // To see the connections between nodes and their work actions.

// Get some data
MATCH (n1)-[r]->(n2) RETURN r, n1, n2 LIMIT 25

MATCH (p:Person) return p limit 2

MATCH (p:Person)-[rel:ACTED_IN]->(m:Movie)
return m,p,rel
limit 10

MATCH (p:Person)-[:ACTED_IN]->(m:Movie)
where m.title = 'The Matrix'
return m,p

MATCH (p:Person)-[:ACTED_IN]->(m:Movie)
where p.name = 'Keanu Reeves'
return m,p

:help match   // cyper syntax



match (movie:Movie)
MATCH (director:Person)-[:DIRECTED]->(movie)
MATCH (director)-[:ACTED_IN]->(movie)
return movie, director

match (movie:Movie)
OPTIONAL MATCH (director:Person)-[:DIRECTED]->(movie)<-[:ACTED_IN]-(director)
return movie, director

#Exercise-1

If person A has a contact B, and B has a contact C, then return the names for A,B,C.

Limit the results to a single result.

(a<>c means, a is not equal c)

MATCH (a:Person)-[rel:HAS_CONTACT]->(b)<-[r:HAS_CONTACT]-(c:Person)
WHERE a <> c
return a,b,c
limit 1

#Exercise-2

contact's if they directed movie

MATCH (a:Person)-[:HAS_CONTACT]-(b)
OPTIONAL MATCH(b)-[:DIRECTED]->(movie)
return a.name,b.name,movie.title

//The persons who starts their names with T letter.

MATCH(someone:Person)
WHERE someone.name > 'T' and someone.name < 'U'
return someone