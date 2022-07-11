# Multi-field mappings
```json lines
PUT /multi-field-testing
{
   "mappings": {
        "properties": {
            "company_type": {"type": "text"},
            "name": {"type": "text"},
            "stock_symbol": {
              "properties": {
                "uuid": {"type": "text"},
                "value": {"type": "text"},
                "image_id": {"type": "text"},
                "permalink": {"type": "text"},
                "entity_def_id": {"type": "text"}
              }
            },        
           "phone_number": {"type": "text"},
            "rank": {"type": "long"},
            "short_description": {"type": "text"},
            "created_at": {"type": "date"},
            "website_url": {"type": "text"},
            "updated_at": {"type": "date"},
            "email": {"type": "keyword"},
            "categories": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword"
                }
              }
            }
        }
   }
}
```

### Example to create document

```json lines
POST /company_profiles/_doc
{
  "company_type": "for_profit",
  "name": "Meta",
  "stock_symbol": {
    "uuid": "8fd30bb3-9eb9-839d-4526-85f82c1bfdf7",
    "value": "FB",
    "image_id": "b0fizfugbmc1sipecugq",
    "permalink": "facebook-ipo--8fd30bb3",
    "entity_def_id": "ipo"
  },
  "phone_number": "(816) 463-4825",
  "rank": 16,
  "short_description": "Meta is a social technology company that enables people to connect, find communities, and grow businesses.",
  "created_at": "2007-05-26T04:22:15Z",
  "website_url": "https://meta.com",
  "updated_at": "2022-06-21T02:10:27Z",
  "email": "contactus@meta.com",
  "categories": ["Augmented Reality","Social Media", "Social Network", "Virtual Reality"]
}
```

### Retrieve Documents
```json lines
GET /company_profiles/_search
{
  "query": {
    "match_all": {}
  }
}
```

### Querying the document using text mapping
```json lines
GET /company_profiles/_search
{
  "query": {
    "match": {
      "categories": "Augmented Reality"
    }
  }
}
```

### Querying the document using keyword mapping on the same field

```json lines

GET /company_profiles/_search
{
  "query": {
    "term": {
      "ingredients.keyword": "Augmented Reality"
    }
  }
}

```