# Arrays

## Arrays of string are considered as a single string.
```json lines
POST /_analyze
{
  "text": ["Strings in array are", "considered as a single string."],
  "analyzer": "standard"
}
```