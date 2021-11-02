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

#### Sorting on multiple columns
```json
{
    "table": "user",
    "columns": "name|color",
    "sort": "^color,name"
}
```
```json
[["John", "red", ["user", [1]]],
 ["Adam", "blue", ["user", [3]],
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

```json
{
    "table": "user_medal",
    "columns": "user.name|medal.name|medal.color"
}
```
```json
[["John", "WIN", "gold", ["user_medal", [1, 1]]],
 ["John", "LAST", "red", ["user_medal", [1, 2]]],
 ["Ken", "WIN", "gold", ["user_medal", [2, 1]]]]
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

### Addition Display Metadata
```json
{
    "table": "user",
    "columns": "user|SUM[IF(EQ(user_medal:user.medal.name,"WIN"),user_medal:user.count,0)]",
    "name": "Scoreboard",
    "info": "The results of all players",
    "column_names": "|Score",
    "column_info": "|The player's win count"
}
```
```json
[["John", 1, ["user", [1]]],
 ["Adam", 5, ["user", [3]],
 ["Ken", 0, ["user", [2]]]]
```
---
*name*, *info*, *column_names* and *column_info*, are ignored by the API itself.
They are used by the UI components.
*name* and *column_names* are optional and, where omitted, will fall back to table level customisations, or be automatically formatted from the table and column names in the database.
The formatting follows these conversions: `table_name` -> `Table Name` and `column_name` -> `column name`.
*info* and *column_info* are typically used for things like tooltips.

## Ideas


### decoration, view, and extra behaviour features

* _valance_display_metadata_table

| *id* | table | name | info | hide |
| ---- | ----- | ---- | ---- | ---- |

* _valance_display_metadata_column

| *id* | table | column | name | info | hide |
| ---- | ----- | ------ | ---- | ---- | ---- |

* _valance_labelled_relationship

| *id* | table | label | relationship |
| ---- | ----- | ----- | ------------ |




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
IF(,,)
```

### result agregators

```
SUM[]
COUNT[]
MIN[]
MAX[]
```
