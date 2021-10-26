# Valance API

## Ideas (WIP)

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
    "table": "mytable",
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
    "table": "mytable",
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
    "table": "mytable",
    "columns": ["name"],
    "offset": 1
}
```
> ```json
> [
>     ["Ken", ["user", 2]]
> ]
> ```
