# All Queries used so far

```json lines
GET /_cluster/health

GET /_cat/indices?v&expand_wildcards=all

GET /_cat/shards?v

PUT /companypeers

GET /_cat/indices?v

POST /_cluster/voting_config_exclusions?node_names=second-node

DELETE /companypeers

DELETE /documents

DELETE /products

PUT /documents
{
  "settings": {
    "number_of_shards": 2,
    "number_of_replicas": 2
  }
}

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

POST /documents/_update/100
{
  "doc": {
    "name":"Ammended Annual Reports"
  }
}

POST /documents/_update/100
{
  "doc": {
    "tags": ["2022", "10KA", "Reports"]
  }
}

PUT /products
{
  "settings": {
    "number_of_replicas": 2,
    "number_of_shards": 2
  }
}

POST /products/_doc/100
{
  "name": "Toaster",
  "price": 35,
  "in_stock": 3,
  "tags": ["electronics"]
}



GET /products/_doc/100

GET /products/_mapping

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

POST /product/_doc
{
  "name": "Juicer2",
  "price": "25",
  "in_stock": "5",
  "tags": ["electronics"]
  
}

POST /products/_update/102
{
  "script": {
    "source": "ctx._source.in_stock++"
  },
  "upsert": {
    "name": "Juicer",
    "price": "50",
    "in_stock": "5",
    "tags": ["electronics"]
  }
}

GET /products/_doc/102

DELETE /_index_template/access_log_template_test


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

GET /company_profiles/_mapping

PUT my-index-000001/_doc/1
{
  "group" : "fans",
  "user" : [ 
    {
      "first" : "John",
      "last" :  "Smith"
    },
    {
      "first" : "Alice",
      "last" :  "White"
    }
  ]
}

user.first = 

GET /company_profiles/_search
{
  "query": {
    "match": {
      "short_description": "123"
    }
  }
}

GET /company_profiles/_search
{
  "query": {
    "term": {
      "email": "contactus@hall-services.com"
    }
  }
}

POST /company_profiles/_doc/
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
  "short_description": "Hall 123 Manufacturing Services is a manufacturing company",
  "created_at": "2019-11-22T08:53:36Z",
  "website_url": "http://hallmanufacturing.net",
  "updated_at": "2019-11-22T08:53:36Z",
  "email": "contactus@hall-services.com"
}


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
  "email": "contactus@meta.com"
}



PUT _index_template/access_log_template_test
{
  "index_patterns": ["as-*-access-logs-*"],
  "template":{
    "settings": {
      "number_of_shards": 2,
      "index.mapping.coerce": false
    }, 
    "mappings": {
      "properties": {
        "@timestamp": {
          "type": "date"
        },
        "version": {
          "type": "integer"
        },
        "method": {
          "type": "keyword"
        },
        "message": {
          "type": "text" 
        },
        "uri": {
          "type": "keyword"
        },
        "http.request.referrer": {
          "type": "keyword"
        },
        "http.response.status_code": {
          "type": "long"
        }
      }
    }
  },
  "priority": 500,
  "version": 3
}



POST /as-sd-morningstar-access-logs-2022-01-01/_doc
{
  "@timestamp":"2022-07-11T13:26:32.211+05:30",
  "@version":1,
  "uri": "/company-profile",
  "method": "GET",
  "http": {
    "request": {
      "referrer": "/source-request-path"
    },
    "response": {
      "status_code": 200
    }
  }, 
  "message":"Get Company profile with company id xyz",
  "thread_name":"restartedMain",
  "level":"DEBUG"
}


POST /as-wc-snp-access-logs-2022-01-01/_doc
{
  "@timestamp":"2022-07-11T13:26:32.211+05:30",
  "@version":1,
  "uri": "/snpcompany-profile",
  "method": "GET",
  "http": {
    "request": {
      "referrer": "/source-request-path"
    },
    "response": {
      "status_code": 200
    }
  }, 
  "message":"Get SNP Company profile with company id xyz",
  "thread_name":"restartedMain",
  "level":"DEBUG"
}


GET /as-sd-morningstar-access-logs-2022-01-01
```