# Project Progress Report - Week 5

## Project Overview

This week, I wrote the functions of CRUD operations using the MongoDB Atlas Data API endpoints that I obtained as a result of my research in the past weeks. As it says in the documentation, they were all POST requests. I will also use the Administration API next week; GET and PUT requests will also be needed. My code has many repetitive structures, so I will write a single base HTTP request function and use this base function for all endpoints to make my customizations.

- **/action/findOne:** Function for finding a document in MongoDB Atlas.

```
{
  "dataSource": "mongodb-atlas",
  "database": "todo",
  "collection": "tasks",
  "filter": {
    "text": "Do the dishes"
  },
  "projection": {
    "status": 1,
    "text": 1
  }
}
```

- **/action/find:** Function for finding multiple documents in MongoDB Atlas.

```
{
  "dataSource": "mongodb-atlas",
  "database": "todo",
  "collection": "tasks",
  "filter": {
    "status": "complete"
  },
  "projection": {
    "text": 1,
    "completedAt": 1
  },
  "sort": {
    "completedAt": 1
  },
  "limit": 10
}
```

- **/action/insertOne:** Function for inserting a document in MongoDB Atlas.

```
{
  "dataSource": "mongodb-atlas",
  "database": "todo",
  "collection": "tasks",
  "document": {
    "status": "open${{ env.BUNDLED_SPEC_FILEPATH }}",
    "text": "Do the dishes"
  }
}
```

- **/action/insertMany:** Function for inserting multiple documents in MongoDB Atlas.

```
{
  "dataSource": "mongodb-atlas",
  "database": "todo",
  "collection": "tasks",
  "documents": [
    {
      "status": "open",
      "text": "Mop the floor"
    },
    {
      "status": "open",
      "text": "Clean the windows"
    }
  ]
}
```

- **/action/updateOne:** Function for updating a document in MongoDB Atlas.

```
{
  "dataSource": "mongodb-atlas",
  "database": "todo",
  "collection": "tasks",
  "filter": {
    "_id": {
      "$oid": "642f1bb5cee4111898828bf6"
    }
  },
  "update": {
    "$set": {
      "status": "complete"
    }
  },
  "upsert": false
}
```

- **/action/updateMany:** Function for updating multiple documents in MongoDB Atlas.

```
{
  "dataSource": "mongodb-atlas",
  "database": "todo",
  "collection": "tasks",
  "filter": {
    "status": "open"
  },
  "update": {
    "$set": {
      "status": "complete"
    }
  }
}
```

- **/action/deleteOne:** Function for deleting a document in MongoDB Atlas.

```
{
  "dataSource": "mongodb-atlas",
  "database": "todo",
  "collection": "tasks",
  "filter": {
    "text": "Do the dishes"
  }
}
```

- **/action/deletMany:** Function for deleting multiple documents in MongoDB Atlas.

```
{
  "dataSource": "mongodb-atlas",
  "database": "todo",
  "collection": "tasks",
  "filter": {
    "status": "complete"
  }
}
```

## References

1. [Pico LTE MicroPython SDK](https://github.com/sixfab/pico_lte_micropython-sdk)

2. [Sixfab Pico LTE](https://docs.sixfab.com/docs/sixfab-pico-lte-introduction)

3. [MongoDB Atlas Data API](https://www.mongodb.com/docs/atlas/app-services/data-api/openapi)

## Conclusion

I added CRUD operations for Data API to my project. Next week, I will simplify these functions into a single base function and include important administration methods in my project.
