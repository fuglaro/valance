# Valance API

## Table Query API

Endpoint: `db/<db-name>/query`

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
{
    "labels": ["color", "name"],
    "values": [["red", "John"],
               ["blue", "Ken"],
               ["blue", "Adam"]],
    "rowrefs": [{"id":1},
                {"id":2},
                {"id":3}],
    "colrefs": [[["user", "color", {"id":1}], ["user", "name", {"id":1}]],
                [["user", "color", {"id":2}], ["user", "name", {"id":2}]],
                [["user", "color", {"id":3}], ["user", "name", {"id":3}]]],
    "ismany": [0, 0]
}
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
{
    "labels": ["name"],
    "values": [["John"]],
    "rowrefs": [{"id":1}],
    "colrefs": [[["user", "name", {"id":1}]]],
    "ismany": [0]
}
```
# XXX UPDATE REST
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
{
    "labels": ["name"],
    "values": [["Ken"],
               ["Adam"]],
    "rowrefs": [{"id":2},
                {"id":3}],
    "colrefs": [[["user", "name", {"id":2}]],
                [["user", "name", {"id":3}]]],
    "ismany": [0]
}
```
---

### Sort Conditions

```json
{
    "table": "user",
    "columns": "name",
    "sort": "color"
}
```
```json
{
    "labels": ["name"],
    "values": [["Ken"],
               ["Adam"],
               ["John"]],
    "rowrefs": [{"id":2},
                {"id":3},
                {"id":1}],
    "colrefs": [[["user", "name", {"id":2}]],
                [["user", "name", {"id":3}]],
                [["user", "name", {"id":1}]]],
    "ismany": [0]
}
```
---

#### Sorting on multiple columns

```json
{
    "table": "user",
    "columns": "name|color",
    "sort": "^color,name"
}
```
```json
{
    "labels": ["name", "color"],
    "values": [["John", "red"],
               ["Adam", "blue"],
               ["Ken", "blue"]],
    "rowrefs": [{"id":1},
                {"id":3},
                {"id":2}],
    "colrefs": [[["user", "name", {"id":1}], ["user", "color", {"id":1}]],
                [["user", "name", {"id":3}], ["user", "color", {"id":3}]],
                [["user", "name", {"id":2}], ["user", "color", {"id":2}]]],
    "ismany": [0, 0]
}
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
{
   "labels": ["name"],
    "values": [["Ken"],
               ["Adam"]],
    "rowrefs": [{"id":2},
                {"id":3}],
    "colrefs": [[["user", "name", {"id":2}]],
                [["user", "name", {"id":3}]]],
    "ismany": [0, 0]
}
```
---

## Advanced Examples

*user*
| *id* | name | color |
| ---- | ---- | ----- |
| 1    | John | red   |
| 2    | Ken  | blue  |
| 3    | Adam | blue  |
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

### Relationship Traversal

Relationship traversal can be utilised in `columns`, `sort` conditions, and `where` filters.

```json
{
    "table": "user_medal",
    "columns": "user.name|medal.name|medal.color"
}
```
```json
{
    "labels": ["user.name", "medal.name", "medal.color],
    "values": [["John", "WIN", "gold"],
               ["John", "LAST", "red"],
               ["Ken", "WIN", "gold"]],
    "rowrefs": [{"user":1, "medal":1},
                {"user":1, "medal":2},
                {"user":2, "medal":1}],
    "colrefs": [[["user", "name", {"id":1}], ["medal", "name", {"id":1}], ["medal", "color", {"id":1}]],
                [["user", "name", {"id":1}], ["medal", "name", {"id":2}], ["medal", "color", {"id":2}]],
                [["user", "name", {"id":2}], ["medal", "name", {"id":1}], ["medal", "color", {"id":1}]]],
    "ismany": [0, 0, 0]
}
```
---

#### Reverse Relationship Traversal

```json
{
    "table": "user",
    "columns": "user_medal:user.count"

}
```
```json
[[[[1, ["medal", 1]],
   [2, ["medal", 2]]], ["user", [1]]],
 [[[3, ["medal", 1]]], ["user", [2]]],
 [[], ["user", [3]]]]
```
---

#### Deep Relationship Traversal

```json
{
    "table": "user",
    "columns": "user_medal:user.medal.color"
}
```
```json
[[[["gold", ["medal", 1]],
   ["red", ["medal", 2]]], ["user", [1]]],
 [[["gold", ["medal", 1]]], ["user", [2]]],
 [[], ["user", [3]]]]
```
---

#### Branching Relationships

```json
{
    "table": "user",
    "columns": "{user_medal:user.medal,user_achievement:user.achievement}.name"
}
```
```json
[[[["WIN", ["medal", 1]],
   ["LAST", ["medal", 2]]], ["user", [1]]],
 [[["WIN", ["medal", 1]],
   ["HERO", ["achievement", 1]]], ["user", [2]]],
 [[], ["user", [3]]]]
```
---

### Column Labels

```json
{
    "table": "user",
    "columns": "user|(Score)SUM[IF(EQ(user_medal:user.medal.name,'WIN'),user_medal:user.count,0)]",
}
```
```json
[["John", 1, ["user", [1]]],
 ["Adam", 5, ["user", [3]],
 ["Ken", 0, ["user", [2]]]]
```
---
Column Labels, exemplified above with `(Score)`, are purely decorative to the API, but can be used by UI elements. These are especially useful with formulas or complex relationship chains.

### Formulas

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
IF(,,)
CONTAINS(,)
LIKE(,)
ILIKE(,)
FILTER(,)
LIMIT(,)
SORT(,)
```

### Result Aggregators

```
SUM[]
COUNT[]
MIN[]
MAX[]
FIRST[]
```

## Ideas

XXX TODO return values as ordered dicts with column or label as key. Good for label feature, good for expanding in UIs, good for internal algorithm. Actually just return labels in the top row. Clean. Cool. Crisp

### Schema

XXX Figure out how to list useful to-many links in schema that will list entries with backref to current entry.

XXX

Different folders having scheme variations such as column labels, column values, etc.
Maybe allowing overrides!


Labeled relationships

Labelled formulas

*_valance_column_label*
| *id* | table | label | column |
| ---- | ----- | ----- | ------ |






