# Index Template and Component Template
```json lines
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
```

### Reading indexd documents

```json lines
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
```