# Valance API

## Basic Examples

*user*
| *id* | name | color |
| ---- | ---- | ----- |
| 1    | John | red   |
| 2    | Ken  | blue  |

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
    "columns": ["color", "name"]
}
```
```json
[["red", "John", ["user", [1]]],
 ["blue", "Ken", ["user", [2]]]]
```
---

### Limit

```json
{
    "table": "user",
    "columns": ["name"],
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
    "columns": ["name"],
    "offset": 1
}
```
```json
[["Ken", ["user", [2]]]]
```
---

### Sort

```json
{
    "table": "user",
    "columns": ["name"],
    "sort": ["color"]
}
```
```json
[["Ken", ["user", [2]]],
 ["John", ["user", [1]]]]
```
---
```json
{
    "table": "user",
    "columns": ["name"],
    "sort": ["^color"]
}
```
```json
[["John", ["user", [1]]],
 ["Ken", ["user", [2]]]]
```
---

### Where Filter

```json
{
    "table": "user",
    "columns": ["name"],
    "where": "EQ(color,'blue')"
}
```
```json
[["Ken", ["user", [2]]]]
```
---

## Relationship Examples

*user*
| *id* | name | color |
| ---- | ---- | ----- |
| 1    | John | red   |
| 2    | Ken  | blue  |
---
*achievements*
| *pk* | userid | medal | count |
| ---- | ------ | ----- | ----- |
|   1  | 1      | gold  | 1     |
|   2  | 2      | gold  | 5     |
|   3  | 2      | pile  | 1     |


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
