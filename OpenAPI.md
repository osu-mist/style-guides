# OpenAPI/Swagger Style Guide ![openapi](https://img.shields.io/badge/openapi-2.0-green.svg)

This is a style guide for writing code in OpenAPI/Swagger using YAML. This includes all APIs created from the
[Express API Skeleton](https://github.com/osu-mist/express-api-skeleton).

## Quoting Conventions

For most cases, it's not necessary to quote the value if the value can be parsed correctly with the defined type/format.

Example:

```yaml
currentPageNumber:
  type: integer
  description: Page number of the returned results
  example: 1

termDescription:
  type: string
  description: Human readable academic term description
  example: Winter 2019

termSeason:
  type: string
  description: Season of the term
  example: Winter
  enum: [Fall, Winter, Summer, Spring]

termStartDate:
  type: string
  description: First day of classes in this term. Format is in YYYY-MM-DD
  format: date
  example: 2019-01-07
```

However, if the value can be parsed differently than the expected type, or the string contains special characters, the value should be quoted.

Example:

```yaml
swagger: '2.0'

authorization:
  name: Authorization
  in: header
  required: true
  type: string
  description: '"Bearer [token]" where [token] is your OAuth2 access token'

calendarYear:
  type: string
  description: A 4-digit calendar year
  pattern: '^\d{4}$'
  example: '2019'

status:
  type: string
  description: HTTP status code
  example: '123'

versions:
  type: array
  collectionFormat: csv
  items:
    type: string
    enum: ['2.1', v2] # only quote the necessary items in enum array
```
