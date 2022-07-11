# Adding Mappings

```json lines
PUT /company_profiles
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
            "email": {"type": "keyword"}
        }
   }
}
```

## Example Query

```json lines
PUT /company_profiles/_doc/1
{
  "company_type": "for_profit",
  "name": "Hall Manufacturing Services",
  "stock_symbol": {
    "uuid": "8fd30bb3-9eb9-839d-4526-85f82c1bfdf7",
    "value": "FB",
    "image_id": "b0fizfugbmc1sipecugq",
    "permalink": "facebook-ipo--8fd30bb3",
    "entity_def_id": "ipo"
  },
  "phone_number": "(816) 463-4825",
  "rank": 1488932,
  "short_description": "Hall Manufacturing Services is a manufacturing company",
  "created_at": "2019-11-22T08:53:36Z",
  "website_url": "http://hallmanufacturing.net",
  "updated_at": "2019-11-22T08:53:36Z",
  "email": "contactus@hall-services.com"
}
```

## Retrieve Mapping

```json lines
GET /company_profiles/_mapping
GET /company_profiles/_mapping/field/name
```

## Add Mapping to existing index

```json lines
PUT /company_profiles/_mapping
{
  "properties": {
    "website_url": {
      "type": "date"
    }
  }
}
```