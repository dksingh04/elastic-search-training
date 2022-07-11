# ReIndexing documents

### Reindexing API
```json lines
POST /_reindex
{
  "source": {
    "index": "source_index"
  },
  "dest": {
    "index": "destination_index"
  }
}

```

### Example create new index

```json lines

PUT /company_profiles_new
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
            "rank": {"type": "keyword"},
            "short_description": {"type": "text"},
            "created_at": {"type": "date"},
            "website_url": {"type": "text"},
            "updated_at": {"type": "date"},
            "email": {"type": "keyword"}
        }
   }
}

```

### GET mappings
```json lines
GET /company_profiles/_mappings

```

### Reindex documents into company_profiles_new

```json lines
POST /_reindex
{
  "source": {
    "index": "company_profiles"
  },
  "dest": {
    "index": "company_profiles_new"
  }
}
```

### Retrieve new documents
```json lines
GET /company_profiles_new/_search
{
  "query": {
    "match_all": {}
  }
}
```

### Removing fields

```json lines
POST /_reindex
{
  "source": {
    "index": "company_profiles",
    "_source": ["company_type", "name", "stock_symbol", "phone_number", "rank", "created_at", "updated_at"]
  },
  "dest": {
    "index": "company_profiles_new"
  }
}
```

### Change field name as well

```json lines
POST /_reindex
{
  "source": {
    "index": "company_profiles"
  },
  "dest": {
    "index": "company_profiles_new"
  },
  "script": {
    "source": """
      # Rename "website_url" field to "web_url"
      ctx._source.web_url = ctx._source.remove("website_url");
    """
  }
}
```

### Giving alias name
```json lines
PUT /company_profiles/_mapping
{
  "properties": {
    "web_url": {
      "type": "alias",
      "path": "website_url"
    }
  }
}
```