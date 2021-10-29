# Valance API

## Ideas (WIP)

### relationship traversal andreverse traversal.
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
MIN[]
MAX[]
```

### Example Database

#### *user*

| id | name | color |
| -- | ---- | ----- |
| 1  | John | red   |
| 2  | Ken  | blue  |

### Example Queries

#### Basic row count query

```json
{
    "table": "user",
}
```
> ```json
> 2
> ```

#### Basic column query

```json
{
    "table": "user",
    "columns": ["color", "name"]
}
```
> ```json
> [
>     ["red", "John", ["user", 1]],
>     ["blue", "Ken", ["user", 2]]
> ]
> ```

#### Basic limited query

```json
{
    "table": "user",
    "columns": ["name"],
    "limit": 1
}
```
> ```json
> [
>     ["John", ["user", 1]]
> ]
> ```

#### Basic offset query

```json
{
    "table": "user",
    "columns": ["name"],
    "offset": 1
}
```
> ```json
> [
>     ["Ken", ["user", 2]]
> ]
> ```
