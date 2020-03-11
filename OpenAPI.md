# OpenAPI/Swagger Style Guide ![openapi](https://img.shields.io/badge/openapi-2.0-green.svg)

This is a style guide for writing code in OpenAPI/Swagger using YAML. This includes all APIs created from the
[Express API Skeleton](https://github.com/osu-mist/express-api-skeleton).

## Filter Query Parameters

Query parameters used for filtering data should appear in the following form:
* `filter[<field>]=<value>`: if `field` and `value` are both a single value and the filter checks for
  strict equality
* `filter[<field>][<operation>]=<value>`: otherwise

`field` is a semantic name for the field being used to filter the resources. If the field
corresponds to an `attribute` of the resource, it should be named after this attribute if possible.
`operation` refers to the operation being applied to filter the resources.

Below is a list of allowed values for `operation`

| `operation` | Description                                    |
| ----------- | ---------------------------------------------- |
| `neq`       | Not equal to                                   |
| `gt`        | Greater than                                   |
| `gte`       | Greater than or equal to                       |
| `lt`        | Less than                                      |
| `lte`       | Less than or equal to                          |
| `oneOf`     | `field` is one of the following                |
| `noneOf`    | `field` is none of the following               |
| `hasSome`   | `field` contains at least one of the following |
| `hasAll`    | `field` contains all of the following          |
| `hasNone`   | `field` contains none of the following         |
| `fuzzy`     | `value` partially matches `field`              |

### Examples

* `filter[name]=John` - Matches all resources with name "John"
* `filter[name][oneOf]=John,Alice,Bob` - Matches all resources with name "John", "Alice", or "Bob"
* `filter[name][fuzzy]=Jo` - Matches all resources whose name partially equals "Jo" such as "Jo",
  "Joe", or "John"
* `filter[parkingSpaces][gte]=5` - Matches all resources with at least 5 parking spaces
* `filter[amenities][some]=pond,pool` - Matches all resources that have a pond or a pool
* `filter[amenities][all]=pond,pool` - Matches all resources that have a pond and a pool

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

termStartDate:
  type: string
  description: First day of classes in this term. Format is in YYYY-MM-DD
  format: date
  example: '2019-01-07'

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

Descriptions for abbreviated words, typically enum values, should use backticks (`) around the abbreviation.

Example:

```yaml
citizen:
  type: string
  enum: [FN, N, R, S, C]
  description: |
    Person's citizen code
    - `FN` - Foreign National
    - `N` - Non Resident Alien
    - `R` - Resident Alien
    - `S` - Substantial Presence Alien
    - `C` - Citizen
```

## Line Length & Multiline Strings

We will now be enforcing a maximum line length of 100 characters.
YAML gives use three options for splitting multiline strings `|`, `>-`, and `>`.
For our purposes we only use the first two `|` and `>-`.

`|` should be used when line breaks in the string need to be **preserved**.
```yaml
sex:
  type: string
  nullable: true
  enum: [M, F, N]
  description: |
    Person's sex code
    - `M` - Male
    - `F` - Female
    - `N` - Non-specified
```

`>-` should be used when line breaks in the string should be **ignored**
```yaml
'409Post':
  description: >-
    The request body resource object's type was invalid or, if a
    client-generated ID was used, a resource already exists with this ID
```

## Result Object & Resource Object

Besides the API specification, we also use the OpenAPI/Swagger file as a part of the API development and integrate it into the integration test. Mostly, it's used to compare the object schema, it's a good practice to always separate the result and resource object if possible.

Example:

```yaml
definitions:
  # Result object with a single resource
  AccountBalanceResult:
    properties:
      links:
        $ref: '#/definitions/SelfLink'
      data:
        $ref: '#/definitions/AccountBalanceResource'
  AccountBalanceResource:
    properties:
      id:
        $ref: '#/definitions/StudentId'
      type:
        type: string
        enum: ['account-balance']
      attributes:
        properties:
          currentBalance:
            type: number
            format: float
            description: Current balance of student's account, in USD.
            example: 2500.39
      links:
        $ref: '#/definitions/SelfLink'

  # Result object with a list of resources must have 'Set' in the name
  AcademicStatusSetResult:
    properties:
      links:
        $ref: '#/definitions/SelfLink'
      data:
        type: array
        items:
          $ref: '#/definitions/AcademicStatusResource'
  AcademicStatusResource:
    properties:
      id:
        $ref: '#/definitions/StudentAndTermId'
      type:
        type: string
        enum: ['academic-status']
      attributes:
        properties:
          academicStanding:
            type: string
            example: Good Standing
            description: Academic standing
            enum:
              - 'Good Standing'
              - 'Academic Dismissal - Graduate'
              - 'Continued Deferred Suspension'
              - 'Honor Roll'
              - 'Academic Probation'
              - 'Special Deferred Suspension'
              - 'Academic Suspension'
              - 'Deferred Suspension'
              - 'Academic Warning'
              - 'Reinstatement After Suspension'
          term:
            description: The term that this course was graded for.
            type: string
            example: '201901'
          termDescription:
            description: Description of the term.
            type: string
            example: 'Fall 2018'
          gpa:
            description: Grade point averages for the given term.
            type: array
            items:
              $ref: '#/definitions/GradePointAverage'
      links:
        $ref: '#/definitions/SelfLink'
```
