## Floating value

```json lines
PUT /coercion_test/_doc/1
{
  "price": 3.14
}
```

## Floating value as String
```json lines
PUT /coercion_test/_doc/2
{
  "price": "3.14"
}
```

## Floating value with invalid string value
```json lines
PUT /coercion_test/_doc/2
{
  "price": "3.14m"
}
```

### document --> "3.14" as string --> apply coercion (Inspect and coerce into field data type if possible) --> 3.14 (float)