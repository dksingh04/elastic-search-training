## Create/Delete Index

```json lines
PUT /companypeers
DELETE /companypeers

PUT /documents
{
  "settings": {
    "number_of_shards": 2,
    "number_of_replicas": 2
  }
}
```

## Add/Get/Update documents to Index

```json lines
POST /documents/_doc
{
  "doctype": "_10K",
  "source": "TKR",
  "name": "Annual Reports"
}

PUT /documents/_doc/100
{
  "doctype": "_10KA",
  "source": "TKR",
  "name": "Ammended Annual Reports2"
}

GET /documents/_doc/100

// Updating Documents

POST /documents/_update/100
{
  "doc": {
    "name":"Ammended Annual Reports"
  }
}
// We can add new field in the existing document.
POST /documents/_update/100
{
  "doc": {
    "tags": ["2022", "10KA", "Reports"]
  }
}
```

## Scripting

```json lines
POST /products/_doc/100
{
  "name": "Toaster",
  "price": 35,
  "in_stock": 3,
  "tags": ["electronics"]
}
//Script
POST /products/_update/100
{
  "script": {
    "source": "ctx._source.in_stock--"
  }
}

POST /products/_update/100
{
  "script": {
    "source": "ctx._source.in_stock=5"
  }
}

POST /products/_update/100
{
  "script": {
    "source": "ctx._source.in_stock -= params.in_stock_quantity",
    "params": {
      "in_stock_quantity": 2
    }
  }
}
```

## Upsert documents

```json lines

POST /products/_update/101
{
  "script": {
    "source": "ctx._source.in_stock++"
  },
  "upsert": {
    "name": "Blender",
    "price": 25,
    "in_stock": 5,
    "tags": ["electronics"]
  }
}
```

## Update by Query
```json lines
POST /products/_update_by_query
{
  "script": {
    "source": "ctx._source.in_stock--"
  },
  "query": {
    "match_all": {}
  }
}
```

## Ignoring versioning conflicts
The conflicts key may be added as a query parameter instead, i.e. ?conflicts=proceed.

```json lines

POST /products/_update_by_query
{
  "conflicts": "proceed",
  "script": {
    "source": "ctx._source.in_stock--"
  },
  "query": {
    "match_all": {}
  }
}
```
## Delete by query
```json lines
POST /products/_delete_by_query
{
  "query": {
    "match_all": { }
  }
}
```

## Ignoring versioning conflicts
The conflicts key may be added as a query parameter instead, i.e. ?conflicts=proceed.
```json lines
POST /products/_delete_by_query
{
  "conflicts": "proceed",
  "query": {
    "match_all": { }
  }
}
```

#Batch Processing

## Indexing documents
```json lines
POST /_bulk
{ "index": { "_index": "products", "_id": 1 } }
{ "name": "Espresso Machine", "price": 199, "in_stock": 5 }
{ "create": { "_index": "products", "_id": 2 } }
{ "name": "Milk Frother", "price": 149, "in_stock": 14 }
```

## Updating and Deleting documents
```json lines
POST /_bulk
{ "update": { "_index": "products", "_id": 2 } }
{ "doc": { "price": 129 } }
{ "delete": { "_index": "products", "_id": 1 } }
```

## Specifying the index name in the query
```json lines
POST /products/_bulk
{ "update": { "_id": 2 } }
{ "doc": { "price": 129 } }
{ "delete": { "_id": 1 } }
```

