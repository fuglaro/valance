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
COUNT[]
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

#### Count

```json
{
    "table": "user"
}
```
> ```json
> 2
> ```

#### Columns

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

#### Limit

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

#### Offset

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

#### Sort

```json
{
    "table": "user",
    "columns": ["name"],
    "sort": ["color"]
}
```
> ```json
> [
>     ["Ken", ["user", 2]],
>     ["John", ["user", 1]]
> ]
> ```
