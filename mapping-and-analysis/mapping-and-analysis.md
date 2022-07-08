## Analyze string by using standard analyzer

```markdown

POST /_analyze
{
  "text": "N Peoples have N viewes some use ElasticSearch and some uses Solr, but underline both uses Lucine!!!, So fundamental is Important!!! :-)",
  "analyzer": "standard"
}
```

```markdown

POST /_analyze
{
  "text": "N Peoples have N viewes some use ElasticSearch and some uses Solr, but underline both uses Lucine!!!, So fundamental is Important!!! :-)",
  "char_filter": [],
  "tokenizer": "standard",
  "filter": ["lowercase"]
}
```