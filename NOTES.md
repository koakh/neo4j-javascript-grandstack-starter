# Notes

## Install

start with [README.md](https://github.com/grand-stack/grand-stack-starter), or read it locally

- create neo4j desktop instance with password `letmein`
- install apoc
- start server, go to detail and confirm ports 
  - Bolt port: 7687
  - HTTP port: 7474
  - HTTPS port: 7473

`api/.env`

```conf
NEO4J_URI=bolt://localhost:7687
NEO4J_USER=neo4j
NEO4J_PASSWORD=letmein
GRAPHQL_LISTEN_PORT=4001
GRAPHQL_URI=http://localhost:4001/graphql
```

```shell
# install deps
$ cd ./ui; npm install; cd ..; cd ./api; npm install
# start API server
$ cd ./api && npm start
# seed database$ cd ./api
$ npm run seedDb
# start UI frontend
$ cd ./ui && npm start
```

## docker compose works with full stack, neo4j, ui and api

> optional, use this to deploy only

```shell
# run docker-compose
$ docker-compose up -d
$ docker-compose run api npm run seedDb
```

> `docker-composer` : change port `- 4000:4000`(nomachine) to `- 4040:4000` to prevent conflicts

## Neo4j

```neo4j
call db.schema();
MATCH(n) RETURN n;
MATCH(n:Category)<--(b:Business) WHERE n.name = 'Coffee' RETURN n,b;
MATCH(n:Category)<--(b:Business)<--(r:Review) WHERE n.name = 'Coffee' RETURN n,b,r;
```

## Sample Queries

enter [playground](http://localhost:4001/graphql)

```graphql
// without arguments
query {
  User {
    name
  }
}

// with arguments
query {
  User(name:"Will")  {
    id
    name
    friends {
      name
    }
    avgStars
    numReviews
  }
}

// with arguments
{
  Category(name: "Coffee") {
    name
    businesses {
      name
      address
      city
      reviews {
        stars
        text
      }
    }
  }
}
```

## Mutations

```
# create user
mutation {
  u5: CreateUser(id: "u5", name: "Kapa") {
    id
    name
  }
}
```

## Postman

```json
{
  "query" : "{User {id name}}"
}
```

```shell
curl -X POST \
  http://localhost:4040/ \
  -H 'Content-Type: application/json' \
  -d '{ "query" : "{User {id name}}" }'
```
