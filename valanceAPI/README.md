# Valance API

## Basic Examples

*user*
| *id* | name | color |
| ---- | ---- | ----- |
| 1    | John | red   |
| 2    | Ken  | blue  |
| 3    | Adam | blue  |

### Count

```json
{
    "table": "user"
}
```
```json
2
```
---

### Columns

```json
{
    "table": "user",
    "columns": "color|name"
}
```
```json
[["red", "John", ["user", [1]]],
 ["blue", "Ken", ["user", [2]]],
 ["blue", "Adam", ["user", [3]]]]
```
---

### Limit

```json
{
    "table": "user",
    "columns": "name",
    "limit": 1
}
```
```json
[["John", ["user", [1]]]]
```
---

### Offset

```json
{
    "table": "user",
    "columns": "name",
    "offset": 1
}
```
```json
[["Ken", ["user", [2]]],
 ["Adam", ["user", [3]]]]
```
---

### Sort

```json
{
    "table": "user",
    "columns": "name",
    "sort": "color"
}
```
```json
[["Ken", ["user", [2]]],
 ["Adam", ["user", [3]],
 ["John", ["user", [1]]]]
```
---
```json
{
    "table": "user",
    "columns": "name|color",
    "sort": "^color|name"
}
```
```json
[["John", "red", ["user", [1]]],
 ["Adam", "blue", ["user", [3]]
 ["Ken", "blue", ["user", [2]]]]
```
---

### Where Filter

```json
{
    "table": "user",
    "columns": "name",
    "where": "EQ(color,'blue')"
}
```
```json
[["Ken", ["user", [2]]],
 ["Adam", ["user", [3]]]
```
---

## Relationship Examples

*user*
| *id* | name | color |
| ---- | ---- | ----- |
| 1    | John | red   |
| 2    | Ken  | blue  |
---
*medal*
| *id* | name | color |
| ---- | ---- | ----- |
| 1    | WIN  | gold  |
| 2    | LAST | red   |
---
*user_medal*
| *user*> | *medal*> | count |
| ------- | -------- | ----- |
| 1       | 1        | 1     |
| 1       | 2        | 2     |
| 2       | 1        | 5     |
---
*achievement*
| *id* | name |
| ---- | ---- |
| 1    | HERO |
---
*user_achievement*
| *user*> | *achievement*> |
| ------- | -------------- |
| 2       | 1              |

## Ideas

### Sorting

"sort": ["^color"]


### relationship traversal andr everse traversal.
pet

owner.name

person

pet:owner.breed

### formulas

```
+(, ...)
-()
*(, ...)
/(,)
>(,)
<(,)
EQ()
NOT()
OR(, ...)
AND(, ...)
```

### result agregators

```
SUM[]
COUNT[]
MIN[]
MAX[]
```
